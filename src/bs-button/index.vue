<template>
  <div class="bs-button"
       :style="{ 'flex-direction': direction }"
       @click="onClick">
    <image class="button-image"
           :src="imageSrc"
           :style="imageStyle"
           v-if="imageSrc && imageSrc.length > 0" />

    <text class="button-title"
          :style="titleStyle"
          v-if="titleText && titleText.length > 0">{{ titleText }}</text>

    <div class="button-badge"
         :style="{'width': badgeWidth}"
         v-if="badgeText && badgeText.length > 0">
      <text class="badge-text">{{ badgeText }}</text>
    </div>
  </div>
</template>

<script>
import {
  Default,
  ControlState,
  ButtonDirection
} from './config'

export default {
  props: {
    // 图标
    image: {
      type: Object,
      default: null
    },
    // 文字
    title: {
      type: Object,
      default: null
    },
    // 文字颜色
    titleColor: {
      type: Object,
      default: null
    },
    // 计数
    badgeValue: {
      type: Number,
      default: 0
    },
    // 当前状态是否选中
    isSelected: {
      type: Boolean,
      default: false
    },
    // 是否禁用
    isDisabled: {
      type: Boolean,
      default: false
    },
    // 图片大小
    imageSize: {
      type: Object,
      default: null
    },
    // 图片和文字的排列方式，默认按行排列
    direction: {
      type: String,
      default: ButtonDirection.row
    },
    // title字体大小
    fontSize: {
      type: Number,
      default: 30
    },
    // title与image的间隔距离
    space: {
      type: Number,
      default: 0
    },
    tag: {
      type: Number,
      default: 0
    }
  },
  data: function () {
    return {

    }
  },
  created: function () {

  },
  computed: {
    state: function () {
      if (this.isDisabled) {
        return ControlState.disabled
      }
      if (this.isSelected) {
        return ControlState.selected
      }

      return ControlState.normal
    },
    badgeText: function () {
      if (this.badgeValue > 99) {
        return '99+'
      }
      if (this.badgeValue <= 0) {
        return ''
      }

      return this.badgeValue.toString()
    },
    badgeWidth: function () {
      const length = this.badgeText.length
      const baseWidth = 28
      const numberWidth = 6

      if (length === 0) {
        return 0
      }

      if (length === 1) {
        return baseWidth
      }

      return baseWidth + (length * numberWidth)
    },

    imageSrc: function () {
      if (this.image) {
        return this.image[this.state] || this.image['normal'] || ''
      }

      return ''
    },
    imageStyle: function () {
      if (this.imageSize) {
        return this.imageSize
      }

      return {
        position: 'absolute',
        top: 0,
        bottom: 0,
        right: 0,
        left: 0
      }
    },
    titleText: function () {
      if (this.title) {
        return this.title[this.state] || this.title['normal'] || ''
      }

      return ''
    },
    titleStyle: function () {
      const me = this

      function getColor (state, defaultColor) {
        if (me.titleColor) {
          const color = me.titleColor[state]

          return color || defaultColor
        }

        return defaultColor
      }

      const normalColor = getColor(ControlState.normal, Default.Title.Color)
      const titleColor = getColor(this.state, normalColor)

      return {
        'color': titleColor,
        'font-size': this.fontSize,
        'margin-left': this.space
      }
    }
  },
  methods: {
    onClick: function () {
      if (this.isDisabled) {
        return
      }

      this.$emit('clicked', {
        tag: this.tag
      })
    }
  }
}
</script>

<style scoped>
.bs-button {
  /*flex-direction: row;*/
  justify-content: center;
  align-items: center;
}

.button-badge {
  position: absolute;
  top: 0px;
  right: 0px;
  height: 28px;
  border-radius: 50%;
  background-color: red;

  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.badge-text {
  color: #ffffff;
  font-size: 20;
  text-align: center;
  /*font-family: "Courier New";*/
}
</style>
