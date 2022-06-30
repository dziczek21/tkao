<template>
  <div class="wrapper">
    <navigation-line :hide-content="hideContent" :menu-fixed="menuFixed" />
    <header-screens ref="headerScreen" @input="hideContent = !hideContent" />
    <div class="wrapper__content">
      <about-screen ref="aboutScreen" />
      <benefit-screen ref="benefitScreen" />
    </div>
  </div>
</template>

<script>
import HeaderScreens from '~/components/HeaderScreen'
import NavigationLine from '~/components/NavigationLine'
import AboutScreen from '~/components/AboutScreen'
import BenefitScreen from '~/components/BenefitScreen'
import SmoothScroll from '~/helpers/smoothScroll'

export default {
  name: 'MainPage',
  components: { NavigationLine, HeaderScreens, AboutScreen, BenefitScreen },
  data () {
    return {
      hideContent: false,
      menuFixed: false
    }
  },
  mounted () {
    window.scrollTo({ top: 0 })
    setTimeout(() => {
      // eslint-disable-next-line no-new
      new SmoothScroll(document, 120, 10)
    }, 1000)
    window.addEventListener('scroll', () => {
      const scrolled = window.scrollY
      if (scrolled) {
        this.menuFixed = true
      } else {
        this.menuFixed = false
      }
    })
  },
  destroyed () {
    window.removeEventListener('scroll', () => {}, true)
  }
}
</script>

<style lang="scss">
 .wrapper {
   background: #101118;
   overflow: hidden;
   &__content {
     background-image: url('/bg.png');
     background-size: cover;
   }
 }
</style>
