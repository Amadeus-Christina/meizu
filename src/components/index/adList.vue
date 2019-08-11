<template>
  <div class="clearfix">
    <div class="fl ad-left">
      <a :href="data[0] && data[0].href"><img class="ad_img" :src="data[0] && data[0].imgUrl" alt=""></a>
    </div>
    <div class="fr">
      <div class="ad-right-top"><a :href="data[1] && data[1].href"><img class="ad_img" :src="data[1] && data[1].imgUrl" alt=""></a></div>
      <div class="clearfix">
        <div class="fl"><a :href="data[2] && data[2].href"><img class="ad_img" :src="data[2] && data[2].imgUrl" alt=""></a></div>
        <div class="fr"><a :href="data[3] &&  data[3].href"><img class="ad_img" :src="data[3] && data[3].imgUrl" alt=""></a></div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="less">
  .ad-left{
    width: 615px;
    height: 450px;
  }
  .ad-right-top{
    width: 616px;
    heigth: 220px;
    margin-bottom: 10px;
  }
  .ad-right-button{
    width:303px;
    height: 220px;
  }
  .ad_img{
    width:100%;
    height: 100%;
  }
</style>
<script>
export default {
  components: {},
  mixins: [],
  name: 'ad-list',
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
  methods: {},
  mounted () {},
  created () {},
  filters: {},
  directives: {},
  beforeDestroy () {},
  destroyed () {}
}
</script>
