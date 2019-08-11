<template>
  <div class="post-wrapper">
    <ul class="clearfix">
      <li v-for="(item,index) in data" :key="index">
        <a :href="item.href">
          <img :src="item.imgUrl" alt="">
        </a>
      </li>
    </ul>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: '',
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
    }
  },
  components: {
  }
}
</script>

<style lang="less" scoped>
  .post-wrapper{
    width: 1240px;
    margin: 10px auto 50px;
    li{
      float: left;
      width: 303px;
      height: 180px;
      margin-right: 9px;
      &:last-child{
        margin-right: 0;
      }
      a{
        transition: opacity 0.3s ease-in-out;
        &:hover{
          opacity: 0.85;
        }
      }
    }
  }
</style>
