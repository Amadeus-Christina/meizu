<template>
  <div class="page">
    <v-header></v-header>
    <div class="swiper-wraper">
      <swiper :data="swiperData"></swiper>
      <swiper-menu :data="menuData"></swiper-menu>
    </div>
    <div class="post-wrapper">
      <post :data="postData"></post>
    </div>
    <div class="index-container">
      <div class="sale">
        <h3 class="title">热卖商品</h3>
        <goodslist :data="hotSaleData"/>
      </div>
    </div>
    <div class="index-container">
      <div class="sale">
        <h3 class="title">手机</h3>
        <ad-list :data="phoneAdData"></ad-list>
        <goodslist :data="phoneSaleData"/>
      </div>
    </div>
    <div class="index-container">
      <div class="sale">
        <h3 class="title">智能配件</h3>
        <ad-list :data="smartAdData"></ad-list>
        <goodslist :data="smartSaleData"/>
      </div>
    </div>
    <v-footer></v-footer>
  </div>
</template>

<script type="text/ecmascript-6">
import axios from 'axios'
import vHeader from '../components/common/header'
import swiper from '../components/index/swiper'
import swiperMenu from '../components/index/swiperMenu'
import post from '../components/index/post'
import goodslist from '../components/index/goodsList'
import adList from '../components/index/adList'
import vFooter from '../components/common/footer'
export default {
  name: 'index',
  components: {
    vHeader,
    swiper,
    swiperMenu,
    post,
    goodslist,
    adList,
    vFooter
  },
  data () {
    return {
      swiperData: [],
      menuData: [],
      postData: [],
      hotSaleData: [],
      phoneSaleData: [],
      smartSaleData: [],
      phoneAdData: [],
      smartAdData: []
    }
  },
  methods: {
    async getSwipterData () {
      const {data} = await axios.get('/api/advertise')
      this.swiperData = data
    },
    async getMenuData () {
      const {data} = await axios.get('/api/menu')
      this.menuData = data
    },
    async getPostData () {
      const {data} = await axios.get('/api/post')
      this.postData = data
    },
    async getHotSaleData () {
      const {data} = await axios.get('/api/hotSale')
      this.hotSaleData = data
    },
    async getPhoneSaleData () {
      const {data} = await axios.get('/api/phoneSale')
      this.phoneSaleData = data
    },
    async getSmartSaleData () {
      const {data} = await axios.get('/api/smartSale')
      this.smartSaleData = data
    },
    async getPhoneAdData () {
      const {data} = await axios.get('/api/phoneRecommend')
      this.phoneAdData = data
    },
    async getSmartAdData () {
      const {data} = await axios.get('/api/smartRecommend')
      this.smartAdData = data
    }
  },
  mounted () {
    this.getSwipterData()
    this.getMenuData()
    this.getPostData()
    this.getHotSaleData()
    this.getPhoneSaleData()
    this.getSmartSaleData()
    this.getPhoneAdData()
    this.getSmartAdData()
  }
}
</script>

<style lang="less" scoped>
  .swiper-wraper{
    width: 1240px;
    height: 500px;
    position: relative;
    margin: 0 auto;
  }
  .index-container{
    width: 1240px;
    margin: 0 auto;
    .title{
      font-size: 30px;
      font-weight: 400;
      margin-bottom: 50px;
    }
    .sale{
      margin-bottom: 50px;
    }
  }
</style>
