<template>
  <transition name="fade">
    <a
      v-if="visible"
      href="#"
      class="back-to-top"
      @click="scroll"
      aria-label="Back to top"
    >
      <arrow-svg />
    </a>
  </transition>
</template>

<script>
import ArrowSvg from '@/assets/icons/arrow.svg?inline'

export default {
  components: {
    ArrowSvg
  },
  data () {
    return {
      visible: false
    }
  },
  mounted () {
    window.addEventListener('scroll', () => {
      this.visible = window.scrollY > 400
    })
  },
  methods: {
    scroll (e) {
      e.preventDefault()
      window.scrollTo({ top: 0, behavior: 'smooth' })
    }
  }
}
</script>

<style>
.back-to-top {
  position: fixed;
  bottom: 0;
  right: 0;
  margin: 40px;
  padding: 8px;
  line-height: initial;
  background-color: #1a72ff;
  text-decoration: none;
  z-index: 1;
  border-radius: 0.25rem;
  box-shadow: 0 0 4px rgba(0,0,0,.14),
    0 4px 8px rgba(0,0,0,.28);
  transition: all 0.3s ease-in-out;
}

.back-to-top:hover,
.back-to-top:focus-visible {
  background-color: #0058e6;
}
</style>
