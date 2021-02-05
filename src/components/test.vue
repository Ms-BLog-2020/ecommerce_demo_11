<nav class="navbar navbar-default navbar-fixed-top navbar-top">
              <div class="home-logo">
                    <img src="https://i.imgur.com/BCXtjMv.png" alt="" id="home-logo"/>
              </div>
              <div class="dropdown ml-auto">
              <ul class="home-navbar">
                <li class="home-navbar-item">
                  <router-link to="/event_page" class="nav-link">
                  櫻花祭活動
                  </router-link>
                </li>
                <li class="home-navbar-item">
                  <router-link to="/login" class="nav-link">
                  登入
                  </router-link>
                </li>
                <li class="home-navbar-item">
                  <button class="btn btn-sm btn-cart" data-toggle="dropdown" data-flip="false">
                    <i class="fa fa-shopping-cart text-dark fa-2x" aria-hidden="true"></i>
                    <span class="badge badge-pill badge-danger" v-if="cart.carts">{{ cart.carts.length }}</span>
                    <span class="sr-only">unread messages</span>
                  </button>
                  <div class="dropdown-menu dropdown-menu-right p-3" style="min-width: 300px" data-offset="400">
                  <h6>已選擇商品</h6>
                  <table class="table table-sm">
                    <tbody>
                      <tr v-for="item in cart.carts">
                        <td class="align-middle text-center">
                          <button type="button" class="btn btn-outline-danger btn-sm" @click="deleteCart(item.id)">
                            <i class="fa fa-trash-o" aria-hidden="true"></i>
                          </a>
                          </button>
                        </td>
                        <td class="align-middle">
                          {{ item.product.title }}
                          <!-- <div class="text-success" v-if="item.coupon">
                            已套用優惠券
                          </div> -->
                        </td>
                        <td class="align-middle">{{ item.qty }}/{{ item.product.unit }}</td>
                        <td class="align-middle text-right">{{ item.final_total }}</td>
                      </tr>
                    </tbody>
                    <tfoot>
                      <tr>
                        <td colspan="3" class="text-right">總計</td>
                        <td class="text-right">{{ cart.total }}</td>
                      </tr>
                    </tfoot>
                  </table>
                  <router-link to="/checkout" class="btn btn-primary btn-block">
                    <i class="fa fa-cart-plus" aria-hidden="true"></i> 結帳去
                  </router-link>
                </div>
                </li>
              </ul>
                
                
              </div>
              
              
              
            </nav>