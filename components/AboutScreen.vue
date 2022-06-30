<template>
  <div class="about">
    <div class="about__image">
      <img class="about__image-img" src="/about/about-image.png" alt="">
    </div>
    <div class="about__content">
      <p class="about__text" :style="computedStyles">
        TKAO is a team which shares a passion for creating unique games and apps in Unity & Unreal Engine. We use the newest technologies to introduce the craziest ideas into the world.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AboutScreen',
  data () {
    return {
      step: 0,
      scrollpos: 0,
      oldScroll: 0

    }
  },
  computed: {
    computedStyles () {
      return { transform: `translate(${-this.scrollpos}%, ${this.scrollpos}%)` }
    }
  },
  mounted () {
    window.addEventListener('scroll', () => {
      const scrolled = window.scrollY
      this.scrollpos = (((this.$el.getBoundingClientRect().top + 100) - scrolled) + scrolled) / 30
    })
  }
}
</script>

<style lang="scss" scoped>
  .about {
    position: relative;
    padding-top: 185px;
    &__image {
      width: 70%;
      &-img {
        width: 100%;
        display: block;
      }
    }
    &__content {
      width: 40%;
      z-index: 3;
      position: absolute;
      top: 250px;
      right: 12%;
    }
    &__text {
      font-weight: 400;
      font-size: 48px;
      transition: transform .1s;
      line-height: 100%;
    }
  }
</style>
