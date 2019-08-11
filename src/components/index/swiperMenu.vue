<template>
  <div class="menu">
    <ul>
      <li v-for="(item,index) in data" :key="index">
        <a :href="item.href">
          {{item.name}}
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
  .menu{
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    width: 303px;
    background-color: rgba(0,0,0,0.5);
    padding-top: 17px;
    li{
      height: 57px;
      line-height: 57px;
      transition: background-color 0.3s;
      &:hover{
        background-color: rgba(0,0,0,0.55);
        a{
          color: #31a5e7;
        }
      }
    }
    a{
      font-size: 16px;
      padding-left: 40px;
      color: #fff;
      transition: color 0.3s;
    }
  }
</style>
