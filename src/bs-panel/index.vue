<template>
  <div class="wrapper">
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
      default: 30
    },
  },
  data: function () {
    return {

    }
  },
  computed: {
    titleStyle () {
      return {
        'color': this.titleColor,
        'font-size': this.titleFontSize
      }
    }
  }
}
</script>

<style scoped>
.wrapper {
  /*flex-direction: row;*/
  justify-content: center;
  align-items: center;
}

.title-bar {
  height: 80;
  padding-left: 20;
  padding-right: 20;
}

.content {
}
</style>
