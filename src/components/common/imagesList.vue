<template>
  <div :class="{'images-wrapper':type === 'small','images-wrapper_big':type === 'big'}">
    <img class="img" :src="data[activeIndex]" alt="">
    <ul class="imgs">
      <li class="imgs-item" :class="{'active': activeIndex === index}" v-for="(item,index) in data" :key="index" @click="changeImage(index)">
        <img :src="item" alt="">
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
      activeIndex: 0
    }
  },
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    },
    type: {
      type: String,
      default: 'small'
    }
  },
  computed: {},
  watch: {},
  methods: {
    changeImage (index) {
      this.activeIndex = index
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
  .images-wrapper{
    text-align: center;
    .img{
      height: 230px;
      margin-top: 20px;
    }
    .imgs{
      overflow: hidden;
      margin: 13px auto 15px;
      .imgs-item{
        display: inline-block;
        height: 40px;
        width: 40px;
        border-radius: 4px;
        margin: 0 4px;
        border: 1px solid #EFEFEF;
        cursor: pointer;
        &.active{
          border-color: #bdbdbd;
        }
        img{
          width: 40px;
          height: 40px;
        }
      }
    }
  }
  .images-wrapper_big{
    text-align: center;
    .img{
      height: 375px;
      margin: 20px auto;
    }
    .imgs{
      overflow: hidden;
      margin-top: 10px;
      .imgs-item{
        display: inline-block;
        height: 75px;
        width: 75px;
        border-radius: 4px;
        margin: 0 5px;
        border: 1px solid transparent;
        cursor: pointer;
        &.active{
          border-color: #dcdcdc;
        }
        img{
          width: 75px;
          height: 75px;
        }
      }
    }
  }
</style>
