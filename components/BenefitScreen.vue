<template>
  <div class="benefit">
    <div class="benefit__header">
      <div :style="computedStyles" class="benefit__title">
        TKAO makes AR experiences work for anyone. Creating true mixed reality is where we shine.  Blend digital and real with us! 😎
      </div>
    </div>
    <div class="benefit__container">
      <div class="benefit__item">
        <div class="benefit__image">
          <img src="/benefit/1.png" alt="">
        </div>
        <div class="benefit__content">
          <div class="benefit__number">
            01
          </div>
          <p class="benefit__text">
            New shading workflow and tools for mixed reality developers and content creators.
          </p>
        </div>
      </div>
      <div class="benefit__item">
        <div class="benefit__image">
          <img src="/benefit/1.png" alt="">
        </div>
        <div class="benefit__content">
          <div class="benefit__number">
            01
          </div>
          <p class="benefit__text">
            New shading workflow and tools for mixed reality developers and content creators.
          </p>
        </div>
      </div>
      <div class="benefit__item">
        <div class="benefit__image">
          <img src="/benefit/1.png" alt="">
        </div>
        <div class="benefit__content">
          <div class="benefit__number">
            01
          </div>
          <p class="benefit__text">
            New shading workflow and tools for mixed reality developers and content creators.
          </p>
        </div>
      </div>
      <div class="benefit__item">
        <div class="benefit__image">
          <img src="/benefit/1.png" alt="">
        </div>
        <div class="benefit__content">
          <div class="benefit__number">
            01
          </div>
          <p class="benefit__text">
            New shading workflow and tools for mixed reality developers and content creators.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BenefitScreen',
  data () {
    return {
      scrollpos: 0
    }
  },
  computed: {
    computedStyles () {
      return { transform: `translate(${-this.scrollpos}%, ${-this.scrollpos}%)` }
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
  .benefit {
    padding: 77px 193px;
    &__title {
      font-weight: 400;
      margin-left: 10px;
      font-size: 48px;
      line-height: 100%;
      max-width: 768px;
    }
    &__item {
      max-width: 208px;
      margin-left: 48px;
    }
    &__image {
      img {
        width: 180px;
        height: 180px;
        display: block;
      }
    }
    &__container {
      display: flex;
      justify-content: space-between;
      margin-top: 100px;
    }
    &__content {
      display: flex;
    }
    &__number {
      font-style: italic;
      font-weight: 700;
      font-size: 24px;
      line-height: 100%;
      opacity: 0.36;
    }
    &__text {
      font-weight: 300;
      font-size: 24px;
      line-height: 120%;
      opacity: .9;
      margin-left: 10px;
    }
  }
</style>
