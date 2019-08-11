<template>
  <div class="">
    <v-header/>
    <div class="order">
      <div class="order-item">
        <h1 class="order-title">收货人信息</h1>
        <ul class="address-list clearfix">
          <li class="address-item fl" :class="{'active':item.checked == true}" v-for="(item,index) in addressData" :key="index" @click="checkAddress(item)">
            <div class="clearfix address-title">
              <div class="fl">{{item.name}}</div>
              <div class="fr">{{item.phone}}</div>
            </div>
            <div class="address-info">
              {{item.province}}
              {{item.city}}
              {{item.district}}
              {{item.street}}
            </div>
            <div class="address-checked" v-show="item.checked">
              <i class="icon-check address-check"></i>
            </div>
          </li>
          <li class="address-item fl address-add">
            <div class="address-add-icon">+</div>
            <div>添加新地址</div>
          </li>
        </ul>
        <div></div>
      </div>
      <div class="order-item">
        <h1 class="order-title">确认订单信息</h1>
        <table class="order-goods">
          <thead>
          <tr>
            <th class="goods-name">商品</th>
            <th class="goods-price">单价</th>
            <th class="goods-number">数量</th>
            <th class="goods-count">小计</th>
            <th class="goods-express">配送方式</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(item,index) in orderData" :key="index">
            <td class="goods-name">
              <img class="goods-name-img" :src="item.imageUrl" alt="">
              <div class="goods-desc">
                <p>{{item.goodsName}}</p>
                <p>{{item.goodsDesc}}</p>
              </div>
            </td>
            <td class="goods-price">￥{{item.goodsPrice}}</td>
            <td class="goods-number">{{item.count}}</td>
            <td class="goods-count">￥{{item.goodsPrice * item.count}}</td>
            <td class="goods-express" :rowspan="orderData.length" v-if="index === 0">快递配送，运费<span class="red">￥0.00</span></td>
          </tr>
          </tbody>
          <tfoot>
          <tr>
            <td colspan="3" class="order-footer">
              备注：<textarea name="" id="" cols="30" rows="10" placeholder="备注..."></textarea>
            </td>
            <td colspan="2" class="order-total">合计：<span class="price">￥{{checkedGoodsPrice}}</span></td>
          </tr>
          </tfoot>
        </table>
      </div>
      <div class="order-item">
        <h1 class="order-title">选择支付方式</h1>
        <div class="order-pay clearfix">
          <div class="pay-item clearfix">
            <h1 class="pay-title fl">支付宝</h1>
            <ul class="pay-content fl clearfix">
              <li>
                <input v-model="payMode" value="huabei" name="pay" type="radio">
                <img src="../assets/images/banks/huabei.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="alipay" name="pay" type="radio">
                <img src="../assets/images/banks/alipay.png" alt="">
              </li>
            </ul>
          </div>
          <div class="pay-item clearfix">
            <h1 class="pay-title fl">微信</h1>
            <ul class="pay-content fl clearfix">
              <li>
                <input v-model="payMode" value="wechat" name="pay" type="radio">
                <img src="../assets/images/banks/wechat.png" alt="">
              </li>
            </ul>
          </div>
          <div class="pay-item clearfix">
            <h1 class="pay-title fl">网上银行</h1>
            <ul class="pay-content fl clearfix pay-bank">
              <li>
                <input v-model="payMode" value="zhongguo" name="pay" type="radio">
                <img src="../assets/images/banks/zhongguo.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="jianshe" name="pay" type="radio">
                <img src="../assets/images/banks/jianshe.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="nongye" name="pay" type="radio">
                <img src="../assets/images/banks/nongye.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="gongshang" name="pay" type="radio">
                <img src="../assets/images/banks/gongshang.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="jiaotong" name="pay" type="radio">
                <img src="../assets/images/banks/jiaotong.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="zhaoshang" name="pay" type="radio">
                <img src="../assets/images/banks/zhaoshang.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="youzheng" name="pay" type="radio">
                <img src="../assets/images/banks/youzheng.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="xingye" name="pay" type="radio">
                <img src="../assets/images/banks/xingye.png" alt="">
              </li>
              <li>
                <input v-model="payMode" value="shanghai" name="pay" type="radio">
                <img src="../assets/images/banks/shanghai.png" alt="">
              </li>
            </ul>
          </div>
          <ul class="order-total-pay fr">
            <li class="clearfix">
              <div class="fl">总金额</div>
              <div class="fr">￥{{checkedGoodsPrice}}</div>
            </li>
            <li class="clearfix">
              <div class="fl">运费</div>
              <div class="fr">￥0.00</div>
            </li>
            <li class="order-line"></li>
            <li class="clearfix">
              <div class="fl">应付</div>
              <div class="fr order-price">￥{{checkedGoodsPrice}}</div>
            </li>
            <li class="clearfix">
              <a href="javascript:" class="btn success fr" @click="pushOrder">下单并支付</a>
            </li>
          </ul>
       </div>
     </div>
    </div>
    <v-footer/>
    <v-dialog :show.sync="dialogShow" :width="360" :height="80" :confirm-button-show="false" :cancel-button-show="false">
      <div>
        <i class="icon-check-circle" style="color: #00c3f5"></i>成功提交订单
      </div>
      <a href="javascript:" @click="goToIndex" class="btn success">返回首页</a>
    </v-dialog>
  </div>
</template>
<script>
import {mapGetters, mapMutations} from 'vuex'
import axios from 'axios'
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
      addressData: [],
      payMode: '',
      dialogShow: false
    }
  },
  props: {},
  computed: {
    orderData () {
      const data = this.$store.state.shopcartData.filter(item => item.checked)
      return data
    },
    ...mapGetters([
      'checkedGoodsPrice'
    ])
  },
  watch: {},
  methods: {
    ...mapMutations([
      'REMOVE_GOODS'
    ]),
    async getAddressData () {
      const {data} = await axios.get('/api/addressData')
      this.addressData = data
    },
    checkAddress (val) {
      this.addressData.forEach(item => {
        item.checked = false
        if (item.id === val.id) {
          item.checked = true
        }
      })
    },
    pushOrder () {
      const date = new Date()
      const address = this.addressData.filter(item => item.checked)[0]
      const data = {
        orderId: date.getTime(),
        address: address,
        orderData: this.orderData,
        price: this.checkedGoodsPrice,
        time: date,
        payMode: this.payMode
      }
      this.REMOVE_GOODS()
      console.log(data)
      this.dialogShow = true
    },
    goToIndex () {
      this.$router.push({
        name: 'Index'
      })
    }
  },
  mounted () {
    this.getAddressData()
  },
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
<style scoped lang="less">
  @import "../assets/sytle/order";
</style>
