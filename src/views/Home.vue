<template>
  <div class="home">
    <sp-slide
      :direction=direction
      :animationText=animationText
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
      direction: 'right',
      spAbbreviation: true,
      animationText: 'hello, this is a banner'
    }
  },
  methods: {
  }
}
</script>
