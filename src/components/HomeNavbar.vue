<template>
    <div>
        <nav class="navbar navbar-green bg-green">
            <div class="text-white"></div>
            <div class="container align-items-center">
            <router-link to="/home" class="navbar-brand mr-4 d-inline-block text-white h6 mb-0" tag="div">
                <img src="@/assets/images/logo.png" alt="" id="homeLogo"/>
            </router-link>
            
            <div class="dropdown ml-auto">
            <router-link to="/home" class="btn btn-sm btn-admin ml-1">
                <i class="fas fa-home text-white fa-lg" aria-hidden="true"></i>
            </router-link>
            <router-link to="/event_page" class="btn btn-sm btn-admin ml-1">
                <i class="fas fa-star text-white fa-lg" aria-hidden="true"></i>
            </router-link>
            <router-link to="/home_coupon" class="btn btn-sm btn-admin ml-1">
                <i class="fas fa-ticket-alt text-white fa-lg" aria-hidden="true"></i>
            </router-link>
                <button
                class="btn btn-sm btn-cart position-relative"
                data-toggle="dropdown"
                data-flip="false"
                >
                <i
                    class="fa fa-shopping-cart text-white fa-lg"
                    aria-hidden="true"
                ></i>
                <span class="badge badge-pill badge-danger position-absolute" v-if="cart.carts">{{cart.carts.length}}</span>
                <span class="sr-only">unread messages</span>
                </button>
                <div
                class="dropdown-menu dropdown-menu-right p-3"
                style="min-width: 400px; z-index: 1050;"
                data-offset="400"
                >
                <h6 class="font-weight-bold">已選擇商品</h6>
                <table class="table table-sm">
                    <tbody>
                    <tr class="py-5" v-for="item in cart.carts" :key="item.id">
                        <td class="align-middle text-center">
                            <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteCart(item.id)">
                            <i class="far fa-trash-alt"></i>
                        </button>
                        </td>
                        <td class="align-middle"><div class="imgBox" :style="'background-image: url('+item.product.imageUrl+');'"></div></td>
                        <td class="align-middle">{{item.product.title}}</td>
                        <td class="align-middle">{{item.qty}} 件</td>
                        <td class="align-middle text-right">${{item.final_total}}</td>
                    </tr>
                    </tbody>
                </table>
                <router-link
                    to="/checkout"
                    class="btn btn-accent btn-block"
                >
                    <i class="fa fa-cart-plus" aria-hidden="true"></i> 結帳去
                </router-link>
                </div>
            </div>
            
            <router-link to="/login" class="btn btn-sm btn-admin ml-2">
                <i class="fas fa-user text-white fa-lg" aria-hidden="true"></i>
            </router-link>
            </div>
        </nav>
    </div>
</template>
<script type="application/javascript">

import $ from 'jquery'; //載入modal





export default {
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
  .navbar-brand.mr-4.d-inline-block.text-white.h6.mb-0 {
    background-color: transparent;
    margin: 0px;
    padding: 0px;
    border: none;
  }
  img#homeLogo {
    width: 45px;
    height: 45px;
    cursor: pointer;
  }
  li.home-navbar-item {
    display: inline-block;
  }
  li.navbar-leftside {
    display: inline-block;
  }
  
  ul.home-navbar {
    margin-bottom: 0px;
  }

  img#home-logo, li.home-navbar-item {
    align-items: center;
  }

  h1.display-3{
    font-size: 36px;
    font-weight: 500;
    letter-spacing: 2px
  }
  p.lead{
    opacity: 0.6
  }
  nav.navbar.navbar-green.bg-green {
    background-color: green;
  }
  nav.navbar {
    transition-duration: 0.5s;
  }
  nav.navbar-default.navbar-fixed-top.navbar-top nav.navbar-brand {
    background-color: none;
  }

  nav.navbar.navbar-default.navbar-fixed-top.navbar-top {
    background-color: green;
  }
  nav.navbar.navbar-default.navbar-fixed-top.navbar-top a {
    color: white;
  }
  nav.navbar.navbar-default.navbar-fixed-top.navbar-top a:hover {
    color: #ff6e3a;
    transition-duration: 0.5s;
  }

  
  </style>
