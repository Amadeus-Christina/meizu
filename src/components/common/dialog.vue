<template>
  <transition name="dialog">
    <div class="dialog-mask" v-show="show">
      <div class="dialog-box">
        <div class="dialog-wrapper" :style="dialogBox">
          <div class="dialog-header" :class="{'dialog-title':title}">
            {{title}}
            <i class="icon-close dialog-close" @click="close"></i>
          </div>
          <div class="dialog-content" :style="dialogContent">
            <slot></slot>
          </div>
          <div class="dialog-footer" v-if="confirmButtonShow || cancelButtonShow">
            <button v-show="confirmButtonShow" class="btn success wd100 mr20" @click="confirm">{{confirmButtonText}}</button>
            <button v-show="cancelButtonShow" class="btn cancel wd100" @click="cancel">{{cancelButtonText}}</button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  components: {},
  mixins: [],
  name: 'vDialog',
  data () {
    return {}
  },
  props: {
    show: {
      type: Boolean,
      default: false
    },
    height: {
      type: Number,
      default: 280
    },
    width: {
      type: Number,
      default: 760
    },
    title: {
      type: String,
      default: ''
    },
    confirmButtonShow: {
      type: Boolean,
      default: true
    },
    cancelButtonShow: {
      type: Boolean,
      default: true
    },
    confirmButtonText: {
      type: String,
      default: '确定'
    },
    cancelButtonText: {
      type: String,
      default: '取消'
    }
  },
  computed: {
    dialogBox () {
      return {
        width: `${this.width}px`
      }
    },
    dialogContent () {
      return {
        height: `${this.height}px`
      }
    }
  },
  watch: {},
  methods: {
    close () {
      this.$emit('update:show', false)
    },
    confirm () {
      this.$emit('confirm')
    },
    cancel () {
      this.$emit('cancel')
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
  @import "../../assets/sytle/dialog";
</style>
