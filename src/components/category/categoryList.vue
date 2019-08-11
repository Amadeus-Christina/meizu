<template>
  <div class="">
    <div v-if="data.length > 0">
      <ul class="clearfix">
        <li @click="clickItem(item)" class="goods-list" v-for="(item,index) in data" :key="index" :class="{'last-child':(index + 1) % 4 ===0}">
          <a :href="item.href">
            <images-list :data="item.colorImageUrls"/>
            <div class="goods-name">{{item.goodsName}}</div>
            <div class="goods-desc">{{item.goodsDesc}}</div>
            <div class="goods-price">
              <i>￥</i>
              {{item.goodsPrice}}
              <span class="lower" v-if="item.lower">起</span>
              <span class="goods-oldprice" v-if="item.oldPrice">{{item.oldPrice}}</span>
            </div>
          </a>
          <div class="goods-new" v-if="item.newProduct">新品</div>
        </li>
      </ul>
    </div>
    <div v-else class="clearfix empty">
      <div class="fl empty-bg"></div>
      <div class="fr empty-desc">
        <div class="title">抱歉没有找到相关商品</div>
        <p>
          建议您：<br>
          1.适当减少筛选条件<br>
          2.尝试其他条件
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import imagesList from '../common/imagesList'
export default {
  components: {
    imagesList
  },
  mixins: [],
  name: '',
  data () {
    return {}
  },
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    }
  },
  computed: {},
  watch: {},
  methods: {
    clickItem (item) {
      this.$emit('clickItem', item)
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
  .goods-list{
    float: left;
    width: 303px;
    height: 416px;
    background-color: #fff;
    cursor: pointer;
    transition: all .3s ease;
    position: relative;
    margin: 10px 9px 0 0;
    overflow: hidden;
    text-align: center;
    &.last-child{
      margin-right: 0;
    }
    &:hover{
      box-shadow: 0 15px 30px 0 rgba(0,0,0,0.1);
    }
  }
  .goods-img{
    height: 230px;
    margin-top: 30px;
  }
  .goods-name{
    margin-bottom: 5px;
    color: #333;
    font-size: 14px;
  }
  .goods-desc{
    font-size: 12px;
    color: #999;
    margin-bottom: 5px;
  }
  .goods-price{
    position: relative;
    display: inline-block;
    padding-left: 14px;
    font-size: 18px;
    color: #c00;
    i{
      font-style: normal;
      font-size: 14px;
      position: absolute;
      left: 0;
      top:3px;
    }
    .lower{
      font-size: 12px;
    }
    .goods-oldprice{
      text-decoration: line-through;
      color: #666;
      font-size: 14px;
      margin-left: 8px;
    }
  }
  .goods-new{
    position: absolute;
    left: 30px;
    top: 30px;
    width: 60px;
    height: 60px;
    line-height: 60px;
    text-align: center;
    border-radius: 50%;
    background: linear-gradient(120deg,#2e74f6,#56bdf9);
    color: #fff;
  }
  .empty{
    width: 335px;
    margin: 120px auto 380px;
    .empty-bg{
      background: url("../../assets/images/xiongmao.png") no-repeat;
      width: 102px;
      height: 135px;
      margin-right: 30px;
    }
    .empty-desc{
      width: 200px;
      .title{
        font-size: 18px;
        color: #00c3f5;
        margin: 15px auto;
      }
    }
  }
</style>
