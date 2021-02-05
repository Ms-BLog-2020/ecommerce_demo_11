<template>
    <div>
        <div class="container-fluid" id="coupon">
        <loading :active.sync="isLoading"></loading>
        <div class="row mb-4 mt-4 ">
            <div class="col-md-4" id="coupon" v-for="item in products" :key="item.id"  v-if="item.category==='早鳥優惠'">
                <div class="flip_wrap">
                    <!-- 实现容器翻转-->
                    <div class="flip">
                        <div class="coupon">
                        <div class="side front shadow-sm bg-white">
                            
                            <div class="inner">
                            <div class="coupon_category">
                                <p id="coupon">{{item.category}}</p>
                            </div>
                            <div class="coupon_line coupon_line_top"> </div>
                            <div class="coupon_title">
                                <h2 id="coupon">{{item.title}}</h2>
                            </div>
                            <div class="coupon_price">
                                <h1 id="coupon"> {{item.price}} 折</h1>
                            </div>
                            <div class="coupon_line coupon_line_bottom"></div>
                            <div class="coupon_date">
                                <p id="coupon">{{item.description}}</p>
                            </div>
                            <div class="coupon_img" style="height: 100%; width: 100%;background-size: cover; background-position: right"
                        :style="{backgroundImage:`url(${item.imageUrl})`}"
                        ></div> 
                            </div>
                            
                           
                        </div>
                        
                        <div class="side back shadow-sm">
                            <div class="inner">
                            <div class="coupon_category">
                                <p id="coupon">{{item.category}}</p>
                            </div>
                            <div class="coupon_line coupon_line_top"></div>
                            <div class="coupon_code">
                                <h2 id="coupon">折扣碼</h2>
                                <h1 id="coupon">{{item.content}}</h1>
                            </div>
                            <div class="coupon_line coupon_line_bottom"> </div>
                            <div class="coupon_date">
                                <p id="coupon">{{item.description}}</p>
                            </div>
                            </div>
                        </div>
                        </div>
                    </div>
                    </div>
                    </div>
        </div>
        </div>

        
    </div>
</template>

<script>
import $ from 'jquery'; //載入modal

export default {
  data() {
    return {
      products: [],
      product: {}, //存放查看更多的Modal資料
      isLoading: false,
      status: {
        loadingItem: '', //存放產品id
      },
      cart: {},
      
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
    productLink(id){
            this.$router.push(`/productdetail/${id}`);
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
    
    
  },
  created() { //取得資料要在這邊設定
    this.getProducts();
    this.getCart(); //把購物車取得回來
  },
};
</script>

<style>
.container#coupon {
  margin: 100px;
}

.col-md-4#coupon {
  padding: 0px 5px;
  margin: 10px 0px;
  
}
.col-md-4#coupon:hover {
  
}

.col-md-4#coupon .flip_wrap {
  width: 100%;
  height: 220px;
  margin: 0px;
  padding: 0px;
  perspective: 800px;
  box-sizing: border-box;
  cursor: pointer;
  
}
.col-md-4#coupon .flip_wrap:hover .flip {
  transform: rotateY(180deg);
}
.col-md-4#coupon .flip {
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  transition: all 1s ease;
  transform-style: preserve-3d;
}
.col-md-4#coupon .side {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  color: black;
  text-align: ceter;
  opacity: 0.5;
  z-index: 33;
  

}
.col-md-4#coupon .side::before {
  content: "";
  width: 80px;
  height: 80px;
  position: absolute;
  border-radius: 50%;
  left: -12%;
  top: -20%;
  background-color: white;
}
.col-md-4#coupon .side::after {
  content: "";
  width: 80px;
  height: 80px;
  position: absolute;
  border-radius: 50%;
  right: -12%;
  top: -20%;
  background-color: white;
}
.col-md-4#coupon .coupon_img {
  position: absolute;
  top: 0px;
  z-index: -11;
  
}
.col-md-4#coupon .inner {
  text-align: center;
  z-index: 33;
}
.col-md-4#coupon .inner .coupon_line {
  border-top: solid 1px black;
  width: 100%;
}
.col-md-4#coupon .inner .coupon_date {
  padding-top: 10px;
}
.col-md-4#coupon .inner .coupon_code {
  padding: 8px;
}
.col-md-4#coupon .inner::before {
  content: "";
  width: 80px;
  height: 80px;
  position: absolute;
  border-radius: 50%;
  left: -12%;
  bottom: -20%;
  background-color: white;
}
.col-md-4#coupon .inner::after {
  content: "";
  width: 80px;
  height: 80px;
  position: absolute;
  border-radius: 50%;
  right: -12%;
  bottom: -20%;
  background-color: white;
}
.col-md-4#coupon .front {
  backface-visibility: hidden;
  font-size: 18px;
  background: transparent;
}
.col-md-4#coupon p#coupon, .col-md-4#coupon h1#coupon, .col-md-4#coupon h2#coupon, .col-md-4#coupon .front .coupon_date{
  margin: 0px;
  padding: 0px;
}
.col-md-4#coupon .front p#coupon {
    padding: 8px;
}
.col-md-4#coupon .front h2#coupon {
    padding: 15px;
    letter-spacing: 3px;
    font-weight: 550;
}
.col-md-4#coupon .front h1#coupon {
    padding-bottom: 15px;
}

.col-md-4#coupon .front::before {
  content: "";
  width: 80px;
  height: 80px;
  position: absolute;
  border-radius: 50%;
  left: -12%;
  bottom: -20%;
  background-color: white;
}
.col-md-4#coupon .back {
  backface-visibility: hidden;
  transform: rotateY(180deg);
  background: #f2f4df;
  padding: 0 36px;
  box-sizing: border-box;
}
.col-md-4#coupon .back .coupon_date{
    margin: 0px;
    padding: 0px;
}
.col-md-4#coupon .back p#coupon {
    padding: 10px;
}
.col-md-4#coupon .back h2#coupon {
    padding: 10px;
}
.col-md-4#coupon .back h1#coupon {
    padding-bottom: 10px;
}


</style>

