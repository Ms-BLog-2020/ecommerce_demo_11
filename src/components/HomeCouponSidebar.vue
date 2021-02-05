<template>
    <div>
        <section class="button sticky-top">
              <div class="container">
                <div class="row  ">

                    <router-link class="col-md-4 col-category" to="/early_bird" tag="div">
                      <h4>早鳥優惠</h4>
                      <div class="line"></div>
                    </router-link>

                    <router-link class="col-md-4 col-category" to="/home_coupon" tag="div">
                      <h4>活動優惠</h4>
                      <div class="line"></div>
                    </router-link>

                    <router-link class="col-md-4 col-category" to="/holiday" tag="div">
                      <h4>節日優惠</h4>
                      <div class="line"></div>
                    </router-link>
                    

                </div>
              </div>
            </section>
    </div>
</template>

<style>
  h4 {
    letter-spacing: 1px;
    padding-top: 5px;
    margin-bottom: 0px;
    cursor: pointer;
  }
</style>

