<template>
  <div class="">
    <v-header/>
    <div class="category-wrapper">
      <div class="bread">
        <span>首页</span>
        <span class="arrow"> > </span>
        <span>全部</span>
        <span class="arrow"> > </span>
        <span class="last-bread">手机</span>
      </div>
      <filter-box :data="filterBoxData" @filter="getQuery"/>
      <sort-box @getKey="getSortKey" @getStock="getSortStock"/>
      <category-list @clickItem="gotoDetail" :data="categoryListData"/>
      <recommend-list :data="recommendList"/>
    </div>
    <v-footer/>
  </div>
</template>
<script>
import vHeader from '../components/common/header'
import vFooter from '../components/common/footer'
import categoryList from '../components/category/categoryList'
import axios from 'axios'
import filterBox from '../components/category/filterBox'
import sortBox from '../components/category/sortBox'
import recommendList from '../components/category/recommendList'
export default {
  components: {
    vHeader,
    vFooter,
    categoryList,
    filterBox,
    sortBox,
    recommendList
  },
  mixins: [],
  name: '',
  data () {
    return {
      categoryListData: [],
      filterBoxData: [],
      categoryListCopy: [],
      recommendList: [],
      currentQuery: null,
      currentStock: null,
      currentKey: null
    }
  },
  props: {},
  computed: {},
  watch: {},
  methods: {
    async getcategoryListData () {
      const {data} = await axios.get('/api/categoryList')
      this.categoryListData = data
      this.categoryListCopy = [].concat(data)
    },
    async getfilterBoxData () {
      const {data} = await axios.get('/api/queryList')
      this.filterBoxData = data
    },
    async getRecommendListData () {
      const {data} = await axios.get('/api/smartSale')
      this.recommendList = data
    },
    getQuery (val) {
      this.currentQuery = val
      this.sortGoods()
    },
    getSortKey (key) {
      this.currentKey = key
      this.sortGoods()
    },
    getSortStock (val) {
      this.currentStock = val
      this.sortGoods()
    },
    sortGoods () {
      this.categoryListData = [].concat(this.categoryListCopy)
      if (this.currentQuery) {
        Object.keys(this.currentQuery).forEach((key) => {
          if (this.currentQuery[key]) {
            this.categoryListData = this.categoryListData.filter((item) => {
              return item.features.indexOf(this.currentQuery[key]) >= 0
            })
          }
        })
      }
      if (this.currentStock) {
        this.categoryListData = this.categoryListData.filter((item) => {
          return item.available
        })
      }
      if (this.currentKey) {
        if (this.currentKey === 'recommend') {
          this.categoryListData.sort((a, b) => {
            return b.shelveTime - a.shelveTime
          })
        } else if (this.currentKey === 'new') {
          this.categoryListData.sort((a, b) => {
            return b.publishedTime - a.publishedTime
          })
        } else if (this.currentKey === 'low') {
          this.categoryListData.sort((a, b) => {
            return b.goodsPrice - a.goodsPrice
          })
        } else if (this.currentKey === 'high') {
          this.categoryListData.sort((a, b) => {
            return a.goodsPrice - b.goodsPrice
          })
        }
      }
    },
    gotoDetail (item) {
      this.$router.push({
        name: 'Detail',
        params: {
          id: item.id
        }
      })
    }
  },
  mounted () {
    this.getcategoryListData()
    this.getfilterBoxData()
    this.getRecommendListData()
  },
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
<style scoped lang="less">
  .category-wrapper{
    width: 1240px;
    margin: 0 auto 60px;
  }
  .bread{
    height: 40px;
    line-height: 40px;
    .arrow,.last-bread{
      color: #999;
    }
  }
</style>
