<template>
  <div class="home">
    <sp-slide
      :direction=direction
      :slideTextList= slideTextList
    >
    </sp-slide>
  </div>
</template>

<script>
// @ is an alias to /src
import spSlide from '@/components/slide.vue'

export default {
  name: 'home',
  components: {
    spSlide
  },
  data () {
    return {
      slideTextList: ['hello, this is a banne', 'zzz', 'dasdsada', 'dasdsad'],
      direction: 'up',
      spAbbreviation: true,
      animationText: 'hello, this is a banner'
    }
  },
  methods: {
  }
}
</script>
