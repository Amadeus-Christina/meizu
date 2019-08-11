<template>
  <div class="clearfix sort-box">
    <div class="fl sort-order">
      <a href="javascript:" @click="setSortKey('recommend')" :class="{'active':activeSortKey === 'recommend'}">推荐</a>
      <a href="javascript:" @click="setSortKey('new')" :class="{'active':activeSortKey === 'new'}">新品</a>
      <a href="javascript:" @click="changePrice" :class="{'active':activeSortKey === 'low'|| activeSortKey === 'high'}">
        价格 <i class="arrow" :class="sortArrow"></i>
      </a>
    </div>
    <div class="fr">
      <input v-model="haveStock" type="checkbox">
      <span>仅显示有货商品</span>
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
      activeSortKey: '',
      activePrice: 'low',
      haveStock: false
    }
  },
  props: {},
  computed: {
    sortArrow () {
      if (this.activePrice === 'low') {
        return 'icon-down'
      } else {
        return 'icon-up'
      }
    }
  },
  watch: {
    haveStock (val) {
      this.$emit('getStock', val)
    }
  },
  methods: {
    setSortKey (val) {
      this.activeSortKey = val
      this.$emit('getKey', this.activeSortKey)
    },
    changePrice () {
      if (this.activeSortKey === this.activePrice) {
        this.activePrice = this.activePrice === 'low' ? 'high' : 'low'
      }
      this.setSortKey(this.activePrice)
    }
  },
  mounted () {
    this.setSortKey('recommend')
  },
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
<style scoped lang="less">
  .sort-box{
    margin: 30px auto 20px;
    color: #666;
    .sort-order{
      a{
        margin-right: 50px;
        &:hover,&.active{
          color: #00c3f5;
          transition: all .2s ease-in-out;
        }
        &:hover .arrow{
          display: inline;
        }
      }
      .arrow{
        display: none;
      }
    }
  }
</style>
