<script setup>
import CloseIcon from './icons/IconClose.vue'
import AvatarDB from './../assets/avatar_data.json'
</script >

<template>
  <div class="avatar-builder">
    <header class="header">
      <button class="header__close-btn">
        <CloseIcon />
      </button>

      <button class="header__set-btn" @click="console.log(finalAvatar)"
        :disabled="Object.keys(finalAvatar).length === 0 || finalAvatar.body === null || finalAvatar.clothes === null || finalAvatar.eyes === null || finalAvatar.ears === null || finalAvatar.head === null">
        Set avatar
      </button>
    </header>

    <main class="main">
      <h2>Create your Buidlbox avatar</h2>

      <output :style="[finalAvatar.grayscale === true ? { 'filter': 'grayscale(1)' } : '']">
        <div :style="{ '--data-url': 'url(./avatar/body/' + finalAvatar.body + ')' }" />
        <div :style="{ '--data-url': 'url(./avatar/clothes/' + finalAvatar.clothes + ')' }" />
        <div :style="{ '--data-url': 'url(./avatar/eyes/' + finalAvatar.eyes + ')' }" />
        <div :style="{ '--data-url': 'url(./avatar/ears/' + finalAvatar.ears + ')' }" />
        <div :style="{ '--data-url': 'url(./avatar/head/' + finalAvatar.head + ')' }" />
        <div :style="{ '--data-url': 'url(./avatar/face/' + finalAvatar.face + ')' }" />
      </output>

      <ul>
        <li><button @click="random()">Random</button></li>
        <li><button @click="grayscale()">grayscale</button></li>
        <li><button @click="reset()">reset</button></li>
      </ul>
    </main>

    <footer class="footer">

      <div class="footer__tabs">
        <ul>
          <li><button @click="activeTab = 'body'" :class="{ active: activeTab === 'body'?true:false }">Body</button></li>
          <li><button @click="activeTab = 'head'" :class="{ active: activeTab === 'head'?true:false }">Head</button></li>
          <li><button @click="activeTab = 'face'" :class="{ active: activeTab === 'face'?true:false }">Face</button></li>
          <li><button @click="activeTab = 'eyes'" :class="{ active: activeTab === 'eyes'?true:false }">Eyes</button></li>
          <li><button @click="activeTab = 'ears'" :class="{ active: activeTab === 'ears'?true:false }">Ears</button></li>
          <li><button @click="activeTab = 'clothes'" :class="{ active: activeTab === 'clothes'?true:false }">Clothes</button></li>
        </ul>
      </div>

      <div class="footer__content">
        <template v-if="activeTab === 'body'">
          <div v-for="(item, index) in AvatarDB.body" :key="index"
            @click="finalAvatar.body = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/body/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'head'">
          <div v-for="(item, index) in AvatarDB.head" :key="index"
            @click="finalAvatar.head = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/head/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'face'">
          <div v-for="(item, index) in AvatarDB.face" :key="index"
            @click="finalAvatar.face = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/face/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'ears'">
          <div v-for="(item, index) in AvatarDB.ears" :key="index"
            @click="finalAvatar.ears = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/ears/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'clothes'">
          <div v-for="(item, index) in AvatarDB.clothes" :key="index"
            @click="finalAvatar.clothes = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/clothes/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'eyes'">
          <div v-for="(item, index) in AvatarDB.eyes" :key="index"
            @click="finalAvatar.eyes = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./avatar/eyes/' + item + ')' }" />
        </template>
      </div>

      <ul class="footer__copyright">
        <li>
          <figure>
            <img src="./../assets/logo.svg" />
          </figure>

        </li>
        <li>
          <span>Made by Buidlbox</span>
        </li>
      </ul>
    </footer>
  </div>
</template>

<style lang="scss" scoped>
.avatar-builder {
  width: 600px;
  min-height: 600px;
  border-radius: 37px;
  background: var(--gradient-primary);
  overflow: hidden;
  display: inline-flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: stretch;
  gap: -30px;
  box-shadow: 0px 0px 38px 0px rgba(0, 0, 0, 0.25);
  user-select: none;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem;

  &__close-btn,
  &__set-btn {
    all: unset;
  }

  &__close-btn {
    background-color: var(--color-white);
    display: flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    border-radius: 999px;
  }

  &__set-btn {
    background-color: var(--color-black);
    color: var(--color-white);
    display: flex;
    align-items: center;
    justify-content: center;
    height: 40px;
    padding: .2rem 1rem;
    border-radius: 999px;
    cursor: pointer;

    &:active {
      &:not([disabled]) {
        transform: scale(.9);
      }
    }

    &[disabled] {
      opacity: .5;
    }
  }
}

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  row-gap: 1rem;

  output {
    position: relative;
    --r: 182px;
    width: var(--r);
    height: var(--r);
    background-color: var(--color-black);
    background-image: url('./../assets/logo-bg.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: 20%;
    border-radius: 999px;

    >div {
      width: 100%;
      height: 100%;
      position: absolute;
      inset: 0;
      border-radius: inherit;
      background-image: var(--data-url);
      background-position: center;
      background-repeat: no-repeat;
      background-size: contain;
    }
  }

  ul {
    display: flex;
    align-items: center;
    justify-content: space-around;
    column-gap: 1rem;
    margin-bottom: 1rem;

    li {
      button {
        background-color: var(--color-background);
        color: #eee;
        padding: .2rem .5rem;
        border-radius: 999px;
        border: none;
        text-transform: capitalize;

        &:active {
          transform: scale(.9);
        }
      }
    }
  }

  h2 {
    color: var(--color-white);
  }
}

.footer {
  background-color: var(--color-footer-background);
  border-top-left-radius: 37px;
  border-top-right-radius: 37px;

  ul {
    display: flex;
  }

  &__tabs {
    padding: 1.5rem 1rem 1rem 1rem;
    border-top-right-radius: inherit;
    border-top-left-radius: inherit;

    ul {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
      row-gap: 1rem;

      li {
        width: 100%;

        button {
          border: none;
          width: 100%;
          height: 100%;
          border-radius: 999px;
          transition: all .1s ease-in-out;

          &:hover {
            opacity: .8;
          }

          &:active {
            transform: scale(.9);
          }

          &.active {
            background: var(--gradient-primary);
            color: var(--white, #fff);
          }
        }
      }
    }
  }

  &__content {
    height: 200px;
    overflow-y: auto;
    color: #fff;
    padding: 1rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;

    div {
      min-height: 62px;
      max-height: 32px;
      background-color: #1B374A;
      background-image: var(--data-url);
      background-repeat: no-repeat;
      background-size: contain;
      background-position: center;
      border-radius: 6px;
      zoom: 2;
      cursor: pointer;

      &:active {
        transform: scale(.9);
      }
    }
  }

  &__more {
    display: flex;
    align-items: center;
    justify-content: center;
    column-gap: 1rem;

    small {
      color: var(--color-primary)
    }
  }

  ul {
    display: flex;
    justify-content: center;
    column-gap: 1rem;
  }

  &__copyright {
    color: #ACACAC;
    padding-bottom: .65rem;
  }
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>

<script>
export default {
  data() {
    return {
      count: 0,
      finalAvatar: ({ body: null, clothes: null, eyes: null, ears: null, head: null, grayscale: false }),
      activeTab: 'body'
    }
  },
  methods: {
    reset() {
      this.finalAvatar = { body: null, clothes: null, eyes: null, ears: null, head: null, grayscale: false }
    },
    random() {
      this.finalAvatar = {
        body: AvatarDB.body[Math.ceil(Math.random() * (AvatarDB.body.length - 1) + 0)],
        clothes: AvatarDB.clothes[Math.ceil(Math.random() * (AvatarDB.clothes.length - 1) + 0)],
        eyes: AvatarDB.eyes[Math.ceil(Math.random() * (AvatarDB.eyes.length - 1) + 0)],
        ears: AvatarDB.ears[Math.ceil(Math.random() * (AvatarDB.ears.length - 1) + 0)],
        head: AvatarDB.head[Math.ceil(Math.random() * (AvatarDB.head.length - 1) + 0)],
        grayscale: this.finalAvatar.grayscale
      }

      console.log(this.finalAvatar)
    },
    grayscale() {
      this.finalAvatar.grayscale = !this.finalAvatar.grayscale
    },
  },
}
</script>