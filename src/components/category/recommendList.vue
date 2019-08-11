<template>
  <div class="">
    <div class="clearfix recommend-header">
      <h3 class="fl title">推荐商品</h3>
      <div class="fr">
        <i class="icon-left pagination-item" @click="prev" :class="{'disabled':activeIndex === 0}"></i>
        <i class="icon-right pagination-item" @click="next" :class="{'disabled':activeIndex === pageSize}"></i>
      </div>
    </div>
    <div v-if="data.length > 0" class="recommend-content">
      <ul class="clearfix" :style="listWrapper">
        <li class="goods-list" v-for="(item,index) in data" :key="index" :class="{'last-child':(index + 1) % 4 ===0}">
          <a :href="item.href">
            <img :src="item.goodsUrl">
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
  </div>
</template>
<script>
export default {
  components: {},
  mixins: [],
  name: '',
  data () {
    return {
      activeIndex: 0
    }
  },
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    }
  },
  computed: {
    listWrapper () {
      return {
        width: `${(this.data.length) * 250}px`,
        transform: `translateX(-${this.activeIndex * 1240}px)`,
        transitionDuration: `.3s`
      }
    },
    pageSize () {
      return Math.floor(this.data.length / 5)
    }
  },
  watch: {},
  methods: {
    prev () {
      if (this.activeIndex === 0) return
      this.activeIndex--
    },
    next () {
      if (this.activeIndex === this.pageSize) return
      this.activeIndex++
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
  .recommend-header{
    margin: 30px auto 10px;
    .title{
      font-size: 30px;
      font-weight: 400;
    }
    .pagination-item{
      display: inline-block;
      width: 24px;
      height: 24px;
      cursor: pointer;
      color: #00c3f5;
      text-align: center;
      line-height: 24px;
      font-size: 12px;
      border: 1px solid #00c3f5;
      &.disabled{
        color: #efefef;
        border-color: #dcdcdc;
      }
    }
  }
  .recommend-content{
    width: 1240px;
    background-color: white;
    overflow: hidden;
    .goods-list{
      float: left;
      width: 220px;
      background-color: #fff;
      cursor: pointer;
      transition: all .3s ease;
      position: relative;
      margin: 0 15px;
      padding: 34px 0 15px;
      overflow: hidden;
      text-align: center;
      img{
        height: 180px;
        &:hover{
          transform: scale(1.2);
          transition: all .3s;
        }
      }
      &.last-child{
        margin-right: 0;
      }
    }
    .goods-name{
      margin-top: 20px;
      margin-bottom: 5px;
      color: #555757;
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
      font-size: 16px;
      color: #c00;
      margin-top: 8px;
      i{
        font-style: normal;
        font-size: 14px;
        position: absolute;
        left: 0;
        top:2px;
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
  }
</style>
