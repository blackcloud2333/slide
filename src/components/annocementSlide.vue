<template>
  <div class="_wrapper">
    <section class="sz-row-flex sz-row-flex-around _boradcard sz-col-6 sz-row-flex-center">
      <!-- 三列布局 -->
      <!--左-->
      <div class="sz-col-flex sz-col-flex-middle">
        <i class="iconfont icon-laba ft36 sz-pdl54 _boradcard__laba" style="flex: none;"></i>
      </div>
      <!--中-->
      <div
        id="_slideText"
        class="_broadcast__text sz-row-flex sz-row-flex-start sz-row-flex-middle sz-col-4"
        :style="{animationDuration:`${animationSpeed}s`}"
        @animationiteration="changeAnimationIndex"
        @animationend="animationend"
      >
        <div class="slide-text" :style="textStyle">{{showText}}</div>
      </div>
      <!-- 右 -->
      <div class="sz-col-1 sz-col-flex sz-col-flex-middle sz-col-flex-center _broadcast__close">
        <i class="iconfont icon-close"></i>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  name: 'slide',
  data () {
    return {
      index: 0, // 多个的时候的index
      showText: '' // 用于滚动的text
    }
  },
  props: {
    animationSpeed: {
      type:Number,
      default:2
    },
    textStyle:{
      type:String,
      default:'',
    }, // 文字的样式
    slideText: {
      type: String,
      default: 'xxx'
    }, // 循环的单条数据
    slideTextList: { 
      type: Array,
      default () {
        return []
      }
    }, // 循环的多条数据
    abbreviation: {
      type: Boolean,
      default: true
    }, // 是否支持缩写，默认支持
    direction: {
      type: String,
      default: 'left'
    } // 支持上下左右
  },
  created () {},
  mounted () {
    this.initBase()
    this.showText = this.slideText
  },
  methods: {
    initBase () {
      let slideText = document.getElementById('_slideText')
      switch (this.direction) {
        case 'left':
          slideText.classList.add('leftSlide')
          break
        case 'right':
          slideText.classList.add('rigthSlide')
          break
        case 'down':
          slideText.classList.add('downSlide')
          break
        case 'up':
          slideText.classList.add('upSlide')
          break
      }
    },
    // 单条数据滚动动画完成之后的钩子
    animationend () {
      this.$emit('on-animationend')
    },
    // 负责多条数据数据的滚动
    changeAnimationIndex () {
      if (this.slideTextList.length >= 1) {
        if (this.index < this.slideTextList.length - 1) {
          this.showText = this.slideTextList[this.index + 1]
          this.index++
        } else {
          this.index = 0
          this.showText = this.slideTextList[0]
        }
      }
    }
  }
}
</script>

// if you don't like it ,you can write by the css
<style lang="scss" scoped>
.slide-text {
  width: 100%;
}
._wrapper {
  background: #d3d3d3;
}
._broadcast {
  &__text {
  }
  &__laba {
    font-size: rem(16);
  }
  &__close {
    font-size: rem(16);
  }
}
.upSlide {
  animation: 3s infinite 1s upSlide;
}
.downSlide {
  animation: 3s infinite 1s downSlide;
}
.leftSlide {
  animation: 3s infinite 1s leftSlide;
}
.rightSlide {
  animation: 3s infinite 1s rightSlide;
}
@keyframes upSlide {
  0% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
  to {
    opacity: 0;
    transform: translate3d(0, -50%, 0);
  }
}
@keyframes downSlide {
  0% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
  to {
    opacity: 0;
    transform: translate3d(0, 50%, 0);
  }
}
@keyframes rightSlide {
  0% {
    opacity: 1;
    transform: translate3d(0%, 0, 0);
  }
  to {
    opacity: 0;
    transform: translate3d(50%, 0, 0);
  }
}
@keyframes leftSlide {
  0% {
    opacity: 1;
    transform: translate3d(50%, 0, 0);
  }
  to {
    opacity: 0;
    transform: translate3d(0%, 0, 0);
  }
}
</style>
