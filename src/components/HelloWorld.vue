
<template>
  <div>
      <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>六角血拼賣賣</title>
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" integrity="sha384-WskhaSGFgHYWDcbwN70/dfYBj47jz9qbsMId/iRN3ewGhXQFZCSftd1LZCfmhktB"
          crossorigin="anonymous">
        <link rel="stylesheet" href="custom.css">
        <!-- Bootstrap CSS 新增加的2020/10/28 -->
        <link href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
        <link rel="preconnect" href="https://fonts.gstatic.com">
        <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC&display=swap" rel="stylesheet">

      </head>

      <body>
        
            
            <HomeNavbar />
            
            <header class="jumbotron jumbotron-fluid jumbotron-bg d-flex align-items-end" id="home">
              <div class="container">
                <div class="p-3 bg-lighter">
                  <h1 class="display-3">給自己品一杯茶的時間</h1>
                  <p class="lead">お茶を楽しむ時間をとってください？</p>
                </div>
              </div>
            </header>

           
            <div class="container main-contant mb-1">
              <div class="row">
                <div class="col-md-12">
                  <Homesidebar></Homesidebar>
                </div>
                <div class="col-md-12">
                  <router-view></router-view>
                </div>
              </div>
            </div>
            <HomeFooter />

            <div class="modal fade" id="removeModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
              <div class="modal-dialog" role="document">
                <div class="modal-content">
                  <div class="modal-header bg-danger text-white">
                    <h5 class="modal-title">刪除商品</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                      <span aria-hidden="true">&times;</span>
                    </button>
                  </div>
                  <div class="modal-body">
                    <p>是否確認刪除商品</p>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-outline-secondary" data-dismiss="modal">否</button>
                    <button type="button" class="btn btn-outline-danger px-5">是</button>
                  </div>
                </div>
              </div>
            </div>
      </body>

    </div>
  </template>
  
  

  
<script type="application/javascript">

import $ from 'jquery'; //載入modal
import Homesidebar from './Homesidebar';
import HomeNavbar from './HomeNavbar';
import HomeFooter from './HomeFooter';

// $('.dropdown-toggle').dropdown();

$(window).scroll(function(evt){
  if($(window).scrollTop()>0)
  $(".navbar").removeClass("navbar-top");
  else
  $(".navbar").addClass("navbar-top")
  
});




export default {
  components: {
        HomeNavbar,
        Homesidebar,
        HomeFooter
  },
  mounted(){
      $(document).ready(function () {
      $('#removeModal').on('show.bs.modal', function (event) {
        var button = $(event.relatedTarget) // 選則當初觸發事件的按鈕
        var title = button.data('title') // 使用 data-* 來取得特定內容

        var modal = $(this)
        modal.find('.modal-title').text('確認' + title) // 寫入資料
      })
    });
  },
  data() {
    return {
      products: [],
      product: {}, //存放查看更多的Modal資料
      isLoading: false,
      status: {
        loadingItem: '', //存放產品id
      },
      cart: {},
      form: { //結構直接參考api設定的資料結構 存放顧客填寫的個人資料
        user: {
          name: '',
          email: '',
          tel: '',
          address: '',
        },
        message: ''
      }
    }
  },
  methods: {
    getProducts() {
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/products/all`;
      vm.isLoading = true;
      this.$http.get(url).then((response) => {
        vm.products = response.data.products;
        console.log(response);
        vm.isLoading = false;
      });
    },
    getProduct(id) {
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${id}`;
      vm.isLoading = true;
      vm.status.loadingItem = id;
      this.$http.get(url).then((response) => {
        vm.product = response.data.product; //先讀取完資料後
        $('#productModal').modal('show'); //再將Modal打開
        console.log(response);
        vm.isLoading = false;  
        vm.status.loadingItem = ''; //Modal打開後將值替換成空的
      });
    },
    addtoCart(id,qty=1){ //ES6 預設值設定方法 qty=1
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
      vm.status.loadingItem = id;
      const cart = { //定義資料結構
        product_id: id,
        qty,
      };
      this.$http.post(url, {data: cart}).then((response) => {
        console.log(response);
        vm.status.loadingItem = ''; //Modal打開後將值替換成空的
        vm.getCart(); //把購物車取得回來
        $('#productModal').modal('hide'); //加到購物車後關掉Modal
      });
    },
    getCart(){
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
      vm.isLoading = true;
      this.$http.get(url).then((response) => {
        vm.cart= response.data.data;
        console.log(response);
        vm.isLoading = false;
      });
    },
    deleteCart(id){
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart/${id}`;
      vm.isLoading = true;
      this.$http.delete(url).then((response) => {
         vm.getCart(); //這部我會忘記做 >> 刪除後重新取得購物車
        console.log(response);
        vm.isLoading = false;
    });
    },
    createOrder(){ //到上方綁定 >> @submit.prevent="createOrder"
      const vm = this;
      const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/order`;
      const order = vm.form; //這部會忘記做
      // vm.isLoading = true;
      this.$validator.validate().then((result)=>{
        if (result){
            this.$http.post(url,{data:order}).then((response) => {
            // vm.getCart(); 
            console.log('訂單已建立',response);
            // vm.isLoading = false;
          })
          }
          else{
            console.log('欄位不完整');
          }
      
      
    });
    },
  },
  created() { //取得資料要在這邊設定
    this.getProducts();
    this.getCart(); //把購物車取得回來
  },
};


     
  </script>

  <style>
  * {
    font-family: 'Noto Serif JP','Noto Serif TC'
  }
  

  header#home.jumbotron {
    text-align: center;
    background-image: url(https://res.klook.com/images/fl_lossy.progressive,q_65/c_fit,w_1295,h_720,f_auto/w_80,x_15,y_15,g_south_west,l_klook_water/activities/q75bagntcomdftmlz0pr/TeaCeremonyinHokkaido.webp);
    background-size: cover;
    background-position:50% 40%;
    background-attachment: fixed;
    margin-bottom: 0px;
    padding: 0px;
    max-height: 520px;
  }
  header#home.jumbotron h4 {
    opacity: 0.6;
    font-weight: normal;
  }
  header#home.jumbotron hr {
    max-width: 60px;
  }
  header#home.jumbotron .container {
    color: white;
    padding: 200px 0px;
    
  }
  section.button{
    padding-top: 30px;
  }
  .col-category {
    padding: 0px;
    display: inline-block;
  }
  .col-category .line {
    height: 1px;
    width: 100%;
    background-color: gray;
    transition-duration: 0.3s;
  }
  .col-category h4 {
    padding-bottom: 10px;
  }
  .col-category:hover h4 {
    color: green;
  }
  .col-category:hover .line {
    background-color: green;
    height: 5px;
  }
  section.button.sticky-top {
    text-align: center;
    padding: 30px 80px;
  }


  </style>





