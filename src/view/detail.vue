<template>
  <div class="bg-white">
    <v-header/>
    <div class="detail-wrapper">
      <div class="bread">
        <span>首页</span>
        <span class="arrow"> > </span>
        <span>全部</span>
        <span class="arrow"> > </span>
        <span class="last-bread">手机</span>
      </div>
      <div class="clearfix">
        <div class="fl detail-images">
          <images-list :data="infoData.colorImageUrls" type="big"/>
        </div>
        <div class="fl detail-props">
          <h1 class="prop-title">{{infoData.goodsName}}</h1>
          <p class="prop-desc">{{infoData.goodsDesc}}</p>
          <div class="prop-sale">
            <span class="prop-name">
              价<span class="prop-space"></span>格：
            </span>
            <span class="prop-price">￥{{infoData.goodsPrice}}</span>
          </div>
          <div>
            <span class="prop-name">
              支<span class="prop-space"></span>持
            </span>
            <ul class="service-list">
              <li class="list-item"><i class="icon-check-circle"></i>百城速达</li>
              <li class="list-item"><i class="icon-check-circle"></i>顺丰包邮</li>
              <li class="list-item"><i class="icon-check-circle"></i>七天无理由</li>
            </ul>
          </div>
          <div>
            <span class="prop-name">
              服<span class="prop-space"></span>务：
            </span>
            <span>本商品由 魅族 负责发货并提供售后服务</span>
          </div>
          <div>
            <span>数量：</span>
            <div class="clearfix prop-number">
              <input class="fl prop-input" v-model="purchaseQuantity" type="number">
              <div class="fl change-box">
                <div class="change-value" @click="increase">+</div>
                <div class="change-value" @click="decrease">-</div>
              </div>
            </div>
          </div>
          <div class="prop-buy">
            <a href="javascript:" class="btn danger mr20" @click="purchase">立即购买</a>
            <a href="javascript:" class="btn success" @click="addShopcart">加入购物车</a>
          </div>
        </div>
      </div>
      <div class="detail-info-wrapper">
        <div class="detail-info">
          <a href="" class="info-title">商品详情</a>
        </div>
        <img class="detail-images" :src="item" alt="" v-for="(item,index) in infoData.information" :key="index">
      </div>
    </div>
    <v-footer/>
    <v-dialog :show.sync="dialogShow" :width="360" :height="80" :confirm-button-show="false" :cancel-button-show="false">
      <div>
        <i class="icon-check-circle add-success"></i>成功加入购物车
      </div>
      <a href="javascript:" @click="goToShopcart" class="go-shopcart">进入购物车</a>
    </v-dialog>
  </div>
</template>
<script>
import axios from 'axios'
import vHeader from '../components/common/header'
import vFooter from '../components/common/footer'
import imagesList from '../components/common/imagesList'
import vDialog from '../components/common/dialog'
export default {
  components: {
    vHeader,
    vFooter,
    imagesList,
    vDialog
  },
  mixins: [],
  name: '',
  data () {
    return {
      infoData: {},
      purchaseQuantity: 1,
      dialogShow: false
    }
  },
  props: {},
  computed: {},
  watch: {},
  methods: {
    async getDetail (id) {
      const {data} = await axios.get(`/api/categoryList/${id}`)
      this.infoData = data
    },
    increase () {
      this.purchaseQuantity = parseInt(this.purchaseQuantity) + 1
    },
    decrease () {
      if (parseInt(this.purchaseQuantity) > 1) {
        this.purchaseQuantity--
      }
    },
    addShopcart () {
      this.$store.commit('ADD_SHOPCART', {
        data: this.infoData,
        num: parseInt(this.purchaseQuantity)
      })
      this.dialogShow = true
    },
    purchase () {
      this.$store.commit('ADD_SHOPCART', {
        data: this.infoData,
        num: parseInt(this.purchaseQuantity)
      })
      this.goToShopcart()
    },
    goToShopcart () {
      this.$router.push({
        name: 'Shopcart'
      })
    }
  },
  mounted () {
    this.getDetail(this.$route.params.id)
  },
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
<style scoped lang="less">
  @import "../assets/sytle/detail";
</style>
