<template>
  <div class="nav" :class="{ loading: isLoading || (hideContent && !menuFixed), 'nav-fixed': menuFixed}">
    <div class="nav__container">
      <nav class="nav__menu menu">
        <ul class="menu__list">
          <li class="menu__item" :class="{ loading: isLoading}">
            <a class="menu__link" href="#">
              <span class="menu__link-text">
                Technology
              </span>
            </a>
          </li>
          <li class="menu__item" :class="{ loading: isLoading}">
            <a class="menu__link" href="#">
              <span class="menu__link-text">
                Portfolio
              </span>
            </a>
          </li>
          <li class="menu__item" :class="{ loading: isLoading}">
            <a class="menu__link" href="#">
              <span class="menu__link-text">
                Developers
              </span>
            </a>
          </li>
          <li class="menu__item" :class="{ loading: isLoading}">
            <a class="menu__link" href="#">
              <span class="menu__link-text">
                Hire us
              </span>
            </a>
          </li>
        </ul>
      </nav>
      <div class="nav-discord">
        <a class="menu__link nav-discord__link" target="_blank" href="#">
          <span class="icon">
            <img src="/icons/discord.svg" alt="Discord">
          </span>
          <span class="nav-discord__text menu__link-text">
            DISCORD
          </span>
        </a>
      </div>
      <div class="nav-discord">
        <a class="menu__link nav-discord__link" target="_blank" href="#">
          <span class="nav-discord__text menu__link-text">
            > TEST VR
          </span>
        </a>
      </div>
      <div class="nav-logo" @click="compact = !compact">
        <div class="nav-logo__container">
          <span class="nav-logo__letter" :class="{ compact: menuFixed }">T</span>
          <span class="nav-logo__letter" :class="{ compact: menuFixed }">K</span>
          <span class="nav-logo__letter" :class="{ compact: menuFixed }">A</span>
          <span class="nav-logo__letter" :class="{ compact: menuFixed }">O</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NavigationLine',
  props: {
    hideContent: {
      type: Boolean,
      default: false
    },
    menuFixed: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      compact: false,
      isLoading: true
    }
  },
  mounted () {
    this.isLoading = false
  }
}
</script>

<style lang="scss">
  .nav {
    &.loading {
      transform: translateY(-100%);
    }
    position: fixed;
    color: #FBFCFE;
    transition: transform 1s;
    transition-delay: 1.5s;
    width: 100%;
    z-index: 10;
    padding: 60px;
    transform: translateY(0%);
    top: 0;
    &__container {
      display: flex;
      justify-content: space-between;
      width: 100%;
    }
    &-discord {
      &__text {
        margin-left: 5px;
      }
      &__link {
        display: flex;
        align-items: center;
        font-weight: 600;
        text-transform: uppercase;
        font-size: 14px;
        line-height: 100%;
      }
    }
    &-logo {
      &__letter {
        font-weight: 700;
        font-size: 24px;
        line-height: 120%;
        display: block;
        transition: all .3s;
        &.compact {
          &:nth-child(1) {
            transform: translate(-42px);
          }
          &:nth-child(2) {
            transform: translate(-29px, -29px);
          }
          &:nth-child(3) {
            transform: translate(-14px, -57px);
          }
          &:nth-child(4) {
            transform: translate(0, -86px);
          }
        }
      }
    }
  }
  .menu {
    &__list {
      margin: 0;
      padding: 0;
      list-style: none;
    }
    &__item {
      margin-bottom: 12px;
    }
    &__link {
      color: #FBFCFE;
      font-weight: 500;
      font-size: 18px;
      line-height: 100%;
      text-decoration: none;
      &-text {
        position: relative;
        &:after {
          content: '';
          background: #FBFCFE;
          width: 0%;
          display: block;
          bottom: 0;
          left: 0;
          height: 1px;
          transition: width .3s;
          position: absolute;
        }
      }
      &:hover {
        .menu__link-text {
          &:after {
            width: 100%;
          }
        }
      }
    }
  }
</style>
