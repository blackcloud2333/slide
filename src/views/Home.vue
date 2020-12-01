<template>
  <div class="home">
    <annocement-slide
      :direction=direction
      :slideTextList="slideTextList"
      :textStyle="textStyle"
      :slideBgcStyle="slideBgcStyle"
      @on-animationend="animationend"
      :animationSpeed=animationSpeed
    >
    </annocement-slide>
  </div>
</template>

<script>
// @ is an alias to /src
import annocementSlide from '@/components/annocementSlide.vue'

export default {
  name: 'home',
  components: {
    annocementSlide
  },
  data () {
    return {
      slideBgcStyle:'background:red',
      // 滚动的周期以秒为单位
      animationSpeed:2,
      //循环滚动的内容的样式
      textStyle:'text-align:center',
      //消失的方向
      direction: 'up',
      //是否支持方向
      abbreviation: true,
      //当有多个数据时
      slideTextList: ['hello, this is a banne', 'zzz', 'dasdsada', 'dasdsad'],
      //当有单条数据时刻 
      slideText: 'hello, this is a banner' 
    }
  },
  methods: {
    animationend () {
    }
  }
}
</script>
