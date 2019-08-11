<template>
  <div class="page">
    <v-header/>
    <div v-if="shopcartData.length > 0" class="shopcart-wrapper">
      <table class="shopcart-header">
        <tr>
          <td class="cart-select">
            <input :checked="isAllChecked" @click="checkAllGoods" type="checkbox" class="cart-checkbox">
            <span>全选</span>
          </td>
          <td class="cart-name">商品</td>
          <td class="cart-price">单价（元）</td>
          <td class="cart-num">数量</td>
          <td class="cart-total">小计（元）</td>
          <td class="cart-operate">操作</td>
        </tr>
      </table>
      <div class="shopcart-list">
        <table>
          <tr v-for="(item,index) in shopcartData" :key="index" class="cart-product">
            <td class="cart-select">
              <input type="checkbox" :checked="item.checked" @click="checkedGoods(item.id)" class="cart-checkbox">
              <img :src="item.imageUrl" alt="" class="cart-img">
            </td>
            <td class="cart-name">
              <span class="cart-title">{{item.goodsName}}</span>
              <span class="cart-desc">{{item.goodsDesc}}</span>
            </td>
            <td class="cart-price">{{item.goodsPrice}}</td>
            <td class="cart-num">
              <div class="cart-input clearfix">
                <button class="fl" @click="decrease(item.id)">-</button>
                <input class="fl" v-model="item.count" type="number">
                <button class="fl" @click="increase(item.id)">+</button>
              </div>
            </td>
            <td class="cart-total">
              ￥{{item.count * item.goodsPrice}}
            </td>
            <td class="cart-operate">
              <i class="icon-close" @click="delGoods(item.id)"></i>
            </td>
          </tr>
        </table>
      </div>
      <div class="clearfix shopcart-footer">
        <div class="fl">
          <input :checked="isAllChecked" @click="checkAllGoods" type="checkbox" class="cart-checkbox">
          <span>全选</span>
          <span class="footer-remove">删除选中的商品</span>
          <span>共 <span class="footer-number gray">{{shopcartTotal}}</span> 件商品，已选 <span class="footer-number blue">{{checkedGoodsTotal}}</span> 件商品</span>
        </div>
        <div class="fr">
          <span>已优惠 <span class="footer-number red">0.00</span>元，合计（不含运费）： <span class="footer-number red footer-total">￥{{checkedGoodsPrice}}</span></span>
          <a href="javascript:" class="btn success" :class="{'cancel':checkedGoodsTotal <=0}" @click="goToOrder">去结算</a>
        </div>
      </div>
    </div>
    <div v-else class="shopcart-empty">
      <div class="empty-content">
        <div class="empty-left"></div>
        <div class="empty-right">
          <p class="empty-desc">购物车内还没有商品，赶紧去选购吧～</p>
          <a href="javascript:" class="btn success" @click="goToIndex">返回商城首页</a>
        </div>
      </div>
    </div>
    <v-footer/>
    <v-dialog :show.sync="dialogShow" title="提示" :width="500" :height="150" @confirm="confirmDelete" @cancel="dialogShow = false">
      <div style="height: 120px;line-height: 120px;">你确定删除该商品吗</div>
    </v-dialog>
  </div>
</template>
<script>
import {mapMutations, mapGetters} from 'vuex'
import vHeader from '../components/common/header'
import vFooter from '../components/common/footer'
import vDialog from '../components/common/dialog'
export default {
  components: {
    vHeader,
    vFooter,
    vDialog
  },
  mixins: [],
  name: '',
  data () {
    return {
      dialogShow: false,
      currentId: null
    }
  },
  props: {},
  computed: {
    ...mapGetters([
      'isAllChecked',
      'checkedGoodsTotal',
      'checkedGoodsPrice',
      'shopcartTotal'
    ]),
    shopcartData () {
      return this.$store.state.shopcartData
    }
  },
  watch: {},
  methods: {
    ...mapMutations([
      'INCREASE_SHOPCART',
      'DECREASE_SHOPCART',
      'CHECK_GOODS',
      'CHECK_ALL_GOODS',
      'DEL_SHOPCART'
    ]),
    increase (id) {
      this.INCREASE_SHOPCART(id)
    //  this.$store.commit('INCREASE_SHOPCART',id)
    },
    decrease (id) {
      this.DECREASE_SHOPCART(id)
    },
    checkedGoods (id) {
      this.CHECK_GOODS(id)
    },
    checkAllGoods () {
      this.CHECK_ALL_GOODS(this.isAllChecked)
    },
    delGoods (id) {
      this.dialogShow = true
      this.currentId = id
      // this.DEL_SHOPCART(id)
    },
    confirmDelete () {
      this.DEL_SHOPCART(this.currentId)
      this.dialogShow = false
    },
    goToIndex () {
      this.$router.push({
        name: 'Index'
      })
    },
    goToOrder () {
      this.$router.push({
        name: 'Order'
      })
    }
  },
  mounted () {},
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
<style scoped lang="less">
  @import "../assets/sytle/shopcart";
</style>
