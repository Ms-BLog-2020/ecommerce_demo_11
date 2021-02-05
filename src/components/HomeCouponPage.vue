
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
            
            <header class="jumbotron jumbotron-fluid jumbotron-bg d-flex align-items-end" id="coupon">
              <div class="container">
                <div class="p-3 bg-lighter">
                  <h1 class="display-3">優惠券獨享專區</h1>
                  <p class="lead">クーポンエリア</p>
                </div>
              </div>
            </header>

           
            <div class="container main-contant mb-1">
              <div class="row">
                <div class="col-md-12">
                  <HomeCouponSidebar></HomeCouponSidebar>
                </div>
                <div class="col-md-12">
                <router-view></router-view>
                 <div class="d-flex justify-content-between">
                    <button class="btn btn-outline-subLight" @click.prevent="beforePath">
                    <i class="fas fa-caret-left"></i> 回到上一頁
                    </button>
                    <router-link to="/home">
                        <button class="btn btn-outline-subLight">
                        前往商品區
                        <i class="fas fa-caret-right"></i> 
                        </button>
                    </router-link>
                </div>
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
import HomeCouponSidebar from './HomeCouponSidebar';
import HomeFooter from './HomeFooter';
import HomeNavbar from './HomeNavbar';

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
        HomeCouponSidebar,
        HomeFooter
  },
  methods: {
    beforePath() {
      this.$router.back()
    }
  }
};


     
  </script>

  <style>
  * {
    font-family: 'Noto Serif JP','Noto Serif TC'
  }
  

  header#coupon.jumbotron {
    text-align: center;
    background-image: url(https://i.imgur.com/JZKvsRR.jpg);
    background-size: cover;
    background-position:50% 50%;
    background-attachment: fixed;
    margin-bottom: 0px;
    max-height: 520px;
    padding: 0px;
  }
  header#coupon.jumbotron h4 {
    opacity: 0.6;
    font-weight: normal;
  }
  header#coupon.jumbotron hr {
    max-width: 60px;
  }
  header#coupon.jumbotron .container {
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





