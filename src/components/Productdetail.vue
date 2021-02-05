<template>
    <div>
        <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300&display=swap" rel="stylesheet">

        </head>

        <HomeNavbar />
        <loading :active.sync="isLoading"></loading>
        <div class="container main-contant mb-1">
            <nav aria-label="breadcrumb" role="navigation">
            <ol class="breadcrumb bg-transparent pl-0 mt-2">
                <li class="breadcrumb-item">
                    <router-link to="/home" class="text-subLight">首頁</router-link>
                </li>
                <!-- <li class="breadcrumb-item">
                    <router-link to="/" class="text-white">{{product.category}}</router-link>
                </li> -->
                <li class="breadcrumb-item active text-subLight" aria-current="page">{{product.title}}</li>
            </ol>
            </nav>
            <div class="row">
                <div class="col-md-8">
                    <img :src="product.imageUrl" class="w-100" alt="">
                </div>
                <div class="col-md-4 mb-5">
                    <div class="sticky-top" style="top: 10px;">
                        <h1 class="h2 text-secondary pt-3">{{product.title}}</h1>
                        <p class="text-secondary">{{product.description}}</p>
                        <span class="tag bg-sub mt-4 ">{{product.category}}</span>
                        
                        <div class="d-flex my-3 align-items-end justify-content-start mb-5">
                            <div class="h4 mb-0 mr-3 text-accent">
                                單價 {{product.price | currency }}
                            </div>
                            <del class="text-secondary">{{product.origin_price | currency}}</del>
                        </div>
                        <p class="card-text text-secondary mt-4">
                            {{product.content}}
                        </p>
                        <select name="" class="form-control mr-1" id="" v-model="product.num">
                            <option v-for="num in 10" :value="num" :key="num">選購 {{num}} {{product.unit}}</option>
                        </select>
                        <div class="form-group mt-3" v-if="product.category ==='茶道體驗'">
                            <label for="due_date">預約體驗日期</label>
                            <input type="date" class="form-control" id="due_date"
                                v-model="product.due_date">
                        </div>
                        <div class="h4 mt-3 text-accent text-right">
                            <span class="h6">總計 </span><strong>{{(product.price * product.num) | currency}}</strong>
                        </div>
                        <hr class="border-white my-4">
                        <div class="d-flex justify-content-between">
                            <router-link to="/home">
                                <button class="btn btn-outline-subLight">
                                <i class="fas fa-caret-left"></i> 回到商品區
                                </button>
                            </router-link>
                            
                            <button href="shoppingCart-checkout.html" class="btn btn-accent"
                                @click="addtoCart(product.id, product.num, product.due_date)" > 
                            <i class="fa fa-cart-plus" aria-hidden="true"></i> 加入購物車
                            </button>
                        </div>
                        <div class="d-flex justify-content-between">
                            <router-link to="/home_coupon">
                                <button class="btn btn-outline-subLight">
                                <i class="fas fa-caret-left"></i> 領取優惠券
                                </button>
                            </router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        
    </div>
</template>

<script>
import HomeNavbar from './HomeNavbar';

export default {
     components: {
        HomeNavbar,
  },
    data() {
        return {
            product: {
                due_date: 0, //把要新添的輸入功能定義資料 並在上方點選購物時 加到購物車內
            },
            isLoading: false,
            cart: {
               
            },
            prodId: '',
        }
    },
    methods: {
        getProduct(){
            const vm = this;
            console.log(vm.prodId)
            const url = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/product/${vm.prodId}`;
            console.log(url)
            vm.isLoading = true;
            this.$http.get(url).then((response) => {
                // console.log(response);
                vm.product = response.data.product;
                vm.$set(vm.product, 'num', 1)
                vm.isLoading = false;
            });
        }, 
        addtoCart (id, qty = 1, due_date) { //將要輸入的資料置入 讓資料傳到購物車內
            const api = `${process.env.APIPATH}/api/${process.env.CUSTOMPATH}/cart`;
            const vm = this;
            vm.isLoading = true;
            const cart = {
                product_id: id,
                qty,
                due_date
            }
            this.$http.post(api, { data: cart }).then((response) => {
                // console.log(response.data)
                vm.$bus.$emit('cartRefresh');
                vm.$bus.$emit('message:push', response.data.message, 'success');
                vm.isLoading = false;
            })
        },
    },
    created(){
        this.prodId = this.$route.params.prodId;
        this.getProduct();
    },
}
</script>

<style scoped>
.card {
  background-color: rgba(255, 255, 255, 0.7) !important;
}
.tag {
  border-radius: 25px 25px 25px 25px;
  background-color: rgba(83, 71, 65, 1);
  color: #fff;
  padding: 2px 4px;
  font-size: 12px;
}
</style>