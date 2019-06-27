<template>
  <div
    class="_wrapper"
    v-show="isShowBroad"
  >
    <section class="sz-row-flex sz-row-flex-around _boradcard sz-col-6 sz-row-flex-center">
      <!-- 三列布局 -->
      <!--左-->
      <div class="sz-col-flex  sz-col-flex-middle">
        <i
          class="iconfont icon-laba ft36 sz-pdl54 _boradcard__laba"
          style="flex: none;"
        >
        </i>
      </div>
      <!--中-->
      <div
        id="_slideText"
        class="rightSlide _broadcast__text sz-row-flex sz-row-flex-start sz-row-flex-middle sz-col-4"
        @animationiteration="changeAnimationIndex"
      >
        <p>
          {{animationText}}
        </p>
      </div>
      <!-- 右 -->
      <div class=" sz-col-1 sz-col-flex sz-col-flex-middle sz-col-flex-center _broadcast__close">
        <i class="iconfont icon-close">
        </i>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  name: 'slide',
  data () {
    return {
      aIndex: '',
      isShowBroad: true
    }
  },
  props: {
    animationText: {
      type: String,
      default: 'xxx'
    },
    slideTextList: {
      type: Object,
      default () {
        return {}
      }
    },
    // 是否支持缩写，默认支持
    spAbbreviation: {
      type: Boolean,
      default: true
    },
    // 支持上下左右
    direction: {
      type: String,
      default: 'left'
    }
  },
  created () {
  },
  mounted () {
    this.initBase()
  },
  methods: {
    // hideBorad () {
    //   this.isShowBroad = false
    // },
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
    changeAnimationIndex () {
      if (this.slideTextList.length >= 1) {
        if (this.aIndex < this.slideTextList.length - 1) {
          this.nowAnimationItem = this.slideTextList[this.aIndex + 1]
          this.aIndex++
        } else {
          this.aIndex = 0
          this.nowAnimationItem = this.slideTextList[0]
        }
      }
    }
  }
}
</script>

// if you don't like it ,you can write by the css
<style lang="scss" scoped>
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
