<template>
  <div class="wrapper"
       :class="classArray">
    <div class="title-bar">
      <text :style="titleStyle">{{ title }}</text>
    </div>

    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    // 文字
    title: {
      type: String,
      default: 'Title'
    },
    // 文字颜色
    titleColor: {
      type: String,
      default: '#000000'
    },

    // title字体大小
    titleFontSize: {
      type: Number,
      default: 34
    },

    // 是否显示顶部边框线
    topBorder: {
      type: Boolean,
      default: false
    },

    // 是否显示底部边框线
    bottomBorder: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    titleStyle () {
      return {
        'color': this.titleColor,
        'font-size': this.titleFontSize
      }
    },

    classArray () {
      var arr = []
      if (this.topBorder) {
        arr.push('line-top')
      }
      if (this.bottomBorder) {
        arr.push('line-bottom')
      }

      return arr
    }
  }
}
</script>

<style scoped>
.wrapper {
  width: 750;
}

.title-bar {
  height: 80;
  padding-left: 20;
  padding-right: 20;
  justify-content: center;
}

.content {
  width: 750;
}

.line-top {
  border-top-width: 1px;
  border-top-color: #dfe1eb;
  border-style: solid;
}

.line-bottom {
  border-bottom-color: #dfe1eb;
  border-bottom-width: 1px;
  border-style: solid;
}
</style>
