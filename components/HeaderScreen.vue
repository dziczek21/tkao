<template>
  <div class="header">
    <div class="header__image" :class="{ loading: isLoading || isVideo }">
      <img class="header__image-img" src="/header/header-image.png" alt="">
    </div>
    <div class="header__video" :class="{ 'header__video-visible': isVideo }">
      <video ref="headerVideo" muted loop src="/header/header-video.mp4" />
      <img class="header__image-img" src="/header/header-image.png" alt="">
    </div>
    <div class="header__container">
      <div class="header__offer" :class="{ loading: isLoading }">
        <span :class="{ loading: isLoading }" :style="{ transform: `translate(${-scrollpos / 40}%, ${scrollpos / 40}%)` }" class="header__offer-word">
          Immersive
        </span>
        <span :class="{ loading: isLoading }" :style="{ transform: `translate(${-scrollpos / 50}%, ${scrollpos / 50}%)` }" class="header__offer-word">
          Technologies
        </span>
        <span :class="{ loading: isLoading }" :style="{ transform: `translate(${-scrollpos / 100}%, ${scrollpos / 100}%)` }" class="header__offer-word">
          Development.
        </span>
      </div>
      <div :class="{ loading: isLoading && !isVideo }" class="header__play">
        <div v-if="!isVideo" class="nav-discord">
          <a class="menu__link nav-discord__link" href="#" @click.prevent="showVideo">
            <span class="icon header__play-icon">
              <img src="/header/header-preview.jpg" alt="Discord">
            </span>
            <span class="nav-discord__text menu__link-text">
              PLAY VIDEO
            </span>
          </a>
        </div>
        <div v-else class="header__play-controls">
          <button class="header__play-stop header__play-button" @click="stopVideo">
            <img src="/icons/stop.svg" alt="">
          </button>
          <button v-if="video.play" class="header__play-stop header__play-button" @click="pauseVideo">
            <img src="/icons/play.svg" alt="">
          </button>
          <button v-else class="header__play-stop header__play-button" @click="playVideo">
            <img src="/icons/pause.svg" alt="">
          </button>
          <button class="header__play-stop header__play-button" @click.prevent="hideContent">
            <span class="menu__link nav-discord__link">
              <span class="nav-discord__text menu__link-text">
                <span v-if="isLoading">SHOW</span><span v-else>HIDE</span> CONTENT &lt;
              </span>
            </span>
          </button>
        </div>
      </div>
      <div class="header__social">
        <div :class="{ loading: isLoading }" class="nav-discord">
          <a class="menu__link nav-discord__link" target="_blank" href="#">
            <span class="icon">
              <img src="/icons/social/twitter.svg" alt="twitter">
            </span>
          </a>
        </div>
        <div :class="{ loading: isLoading }" class="nav-discord">
          <a class="menu__link nav-discord__link" target="_blank" href="#">
            <span class="icon">
              <img src="/icons/social/youtube.svg"  alt="twitter">
            </span>
          </a>
        </div>
        <div :class="{ loading: isLoading }" class="nav-discord">
          <a class="menu__link nav-discord__link" target="_blank" href="#">
            <span class="icon">
              <img src="/icons/social/instagram.svg" alt="twitter">
            </span>
          </a>
        </div>
      </div>
      <div :class="{ loading: isLoading }" class="header__mouse">
        <div class="header__mouse-text" :class="{ 'nobg': isVideo }">
          XR solutions from concept & design to development and support.
        </div>
        <div class="header__mouse-icon">
          <img src="/icons/mouse.svg" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeaderScreens',
  data () {
    return {
      isLoading: true,
      isVideo: false,
      step: 0,
      scrollpos: 0,
      video: {
        play: false
      }
    }
  },
  mounted () {
    setTimeout(() => {
      this.isLoading = false
    }, 100)
    setTimeout(() => {
      window.addEventListener('scroll', () => {
        const scrolled = window.scrollY
        this.scrollpos = ((this.$el.getBoundingClientRect().top + 100) - scrolled)
      })
    }, 300)
  },
  methods: {
    playVideo () {
      this.video.play = true
      this.$refs.headerVideo.play()
    },
    pauseVideo () {
      this.video.play = false
      this.$refs.headerVideo.pause()
    },
    stopVideo () {
      this.$refs.headerVideo.currentTime = 0
      this.video.play = true
    },
    hideContent () {
      this.isLoading = !this.isLoading
      this.$emit('input')
    },
    showVideo () {
      this.isVideo = true
      this.video.play = true
      this.$refs.headerVideo.play()
    }
  }
}
</script>

<style lang="scss" scoped>
  .header {
    height: 102vh;
    background: #101118;
    color: #FBFCFE;
    overflow: hidden;
    position: relative;
    &__video {
      width: 100%;
      height: 100%;
      opacity: 0;
      z-index: 1;
      top: 0;
      transition: opacity .3s;
      left: 0;
      position: absolute;
      &.header__video-visible {
        opacity: 1;
      }
      video {
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: center center;
        display: block;
      }
    }
    &__mouse {
      position: absolute;
      left: 34%;
      bottom: 228px;
      opacity: 1;
      transition: all .5s;
      transition-delay: 1.7s;
      &.loading {
        opacity: 0;
      }
      &-text {
        width: 176px;
        height: 108px;
        background: #101118;
        padding: 10px;
        &.nobg {
          background: transparent;
        }
      }
      &-icon {
        margin-top: 10px;
        margin-left: 10px;
      }
    }
    &__social {
      position: absolute;
      bottom: 60px;
      right: 60px;
      .nav-discord {
        transform: translateY(0%);
        transition: all .5s;
        transition-delay: 1s;
        opacity: 1;
        &.loading {
          opacity: 0;
          transform: translateY(1000%);
        }
        margin-top: 36px;
      }
    }
    &__play {
      position: absolute;
      bottom: 44px;
      left: 60%;
      transition: opacity .3s;
      transition-delay: 1.4s;
      opacity: 1;
      &.loading {
        opacity: 0;
      }
      &-button {
        background: none;
        cursor: pointer;
        border: none;
      }
      &-icon {
        overflow: hidden;
        border-radius: 50%;
        width: 48px;
        height: 48px;
        img {
          width: 100%;
          object-fit: cover;
          object-position: center center;
        }
      }
    }
    &__offer {
      position: absolute;
      bottom: 60px;
      opacity: 1;
      transition: all .5s;
      &.loading {
        opacity: 0;
        transition: all .8s;
      }
      &-word {
        display: block;
        transform: translateX(0%);
        font-weight: 500;
        font-size: 72px;
        line-height: 100%;
      }
    }
    &__container {
      padding: 60px;
      position: relative;
      z-index: 2;
      height: 100%;
    }
    &__image {
      &.loading {
        opacity: 0;
      }
      position: absolute;
      opacity: 1;
      z-index: 1;
      top: 50%;
      transition: opacity .5s;
      width: 60%;
      left: 50%;
      max-height: 100vh;
      transform: translate(-50%, -50%);
      &-img {
        width: 100%;
        height: 100%;
        display: block;
      }
    }
  }
</style>
