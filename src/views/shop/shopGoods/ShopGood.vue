<template>
  <div class="shopGood">
    <div class="menu-wrapper" ref="menuWrapper">
      <ul>
        <li class="menu-item" v-for="(good,index) in goods" :key="index"><!--current选中的样式-->
          <span class="text">
            <img class="icon" v-if="good.icon" v-bind:src="good.icon">
            {{good.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul>
        <li class="food-list-hook" v-for="(good,index) in goods" :key="index">
          <h1 class="title">{{good.name}}</h1>
          <ul>
            <li class="food-item" v-for="(food, index) in good.foods" :key="index">
              <div class="icon">
                <img width="57" height="57" v-bind:src="food.icon">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售 {{food.sellCount}} 份</span>
                  <span>好评率 {{food.rating}}%</span></div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-if="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
                <div class="cartcontrol-wrapper">
                  <CartControl></CartControl>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <ShopCart></ShopCart><!-- 购物车 -->
    <Food></Food><!--商品详情弹框-->
  </div>
</template>

<script>
  import {mapState} from 'vuex'
  import CartControl from "../../../components/cartControl/CartControl"
  import ShopCart from "../../../components/shopCart/ShopCart"
  import Food from "../../../components/food/Food"
  export default {
    name: "ShopGood",
    components:{
      CartControl,
      ShopCart,
      Food
    },
    data(){
      return{

      }
    },
    mounted() {
      this.$store.dispatch('getShopGoods')
    },
    computed:{
      ...mapState(['goods'])
    }
  }
</script>

<style type="text/scss" lang="scss" scoped>
.shopGood{
  display: flex;
  position: absolute;
  top: 203px;
  bottom: 46px;
  width: 100%;
  background: #fff;
  overflow: hidden;
  .menu-wrapper{
    flex: 0 0 80px;
    width: 80px;
    background: #f3f5f7;
    .menu-item{
      display: table;
      height: 54px;
      width: 56px;
      padding: 0 12px;
      line-height: 14px;
      &.current{
        position: relative;
        z-index: 10;
        margin-top: -1px;
        background: #fff;
        color: #02a774;
        font-weight: 700;
        .text{
          border:none;
        }
      }
      .text{
        display: table-cell;
        width: 56px;
        vertical-align: middle;
        border-bottom:1px solid rgba(7, 17, 27, 0.1);
        font-size: 12px;
      }
      .icon{
        display: inline-block;
        vertical-align: top;
        width: 12px;
        height: 12px;
        margin-right: 2px;
        background-size: 12px 12px;
        background-repeat: no-repeat;
      }
    }
  }
  .foods-wrapper{
    flex: 1;
    .title{
      padding-left: 14px;
      height: 26px;
      line-height: 26px;
      border-left: 2px solid #d9dde1;
      font-size: 12px;
      color: rgb(147, 153, 159);
      background: #f3f5f7;
    }
    .food-item{
      display: -webkit-box;
      display: -ms-flexbox;
      display: flex;
      margin: 18px;
      padding-bottom: 18px;
      position: relative;
      border: none;
      &:last-child{
        margin-bottom: 0;
        border:none;
      }
      .icon{
        flex: 0 0 57px;
        margin-right: 10px;
      }
      .content{
        flex: 1;
        .name{
          margin: 2px 0 8px 0;
          height: 14px;
          line-height: 14px;
          font-size: 14px;
          color: rgb(7, 17, 27);
        }
        .desc, .extra{
          line-height: 10px;
          font-size: 10px;
          color: rgb(147, 153, 159);
        }
        .desc{
          line-height: 12px;
          margin-bottom: 8px;
        }
        .extra{
          display: flex;
          .count{
            flex: 1;
          }
        }
        .price{
          font-weight: 700;
          line-height: 24px;
          .now{
            margin-right: 8px;
            font-size: 14px;
            color: rgb(240, 20, 20);
          }
          .old{
            text-decoration: line-through;
            font-size: 10px;
            color: rgb(147, 153, 159);
          }
        }
        .cartcontrol-wrapper{
          position: absolute;
          right: 0;
          bottom: 12px;
        }
      }
    }
  }
}
</style>
