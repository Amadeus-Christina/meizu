<template>
  <div class="filter-box">
    <ul>
      <li class="box-item clearfix" v-for="(item,index) in data" :key="index">
        <div class="fl filter-title">{{item.name}}：</div>
        <ul class="clearfix">
          <li class="filter-item fl" :class="{'active':activeFilter[item.key] === info.value}" v-for="(info,ii) in item.queryList" :key="ii" @click="changeFilter(item.key,info.value)">
            {{info.name}}
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  components: {},
  mixins: [],
  name: '',
  data () {
    return {
      activeFilter: {}
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
  computed: {},
  watch: {},
  methods: {
    changeFilter (key, val) {
      this.$set(this.activeFilter, key, val)
      this.$emit('filter', this.activeFilter)
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
  .filter-box{
    background: white;
    padding: 15px 10px;
    border: 1px solid #efefef;
    .box-item{
      line-height: 46px;
      .filter-title{
        width: 85px;
        padding-left: 10px;
        white-space: nowrap;
        color: #333;
        overflow: hidden;
      }
      .filter-item{
        cursor: pointer;
        margin-right: 62px;
        &.active{
          color: #00c3f5;
        }
      }
    }
  }
</style>
