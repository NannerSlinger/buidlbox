<script setup>
import { ref } from 'vue'
import CloseIcon from './icons/IconClose.vue'
import AvatarDB from './../assets/avatar_data.json'
const count = ref(0)
const finalAvatar = ref({ "body": null, "clothes": null, "eyes": null, "ears": null, "head": null })
const activeTab = ref('body')

// Store in Localstorage
</script>

<template>
  <div class="avatar-builder">
    <header class="header">
      <button class="header__close-btn">
        <CloseIcon />
      </button>

      <button class="header__set-btn" @click="console.log(finalAvatar)"
        :disabled="finalAvatar.body === null || finalAvatar.clothes === null || finalAvatar.eyes === null || finalAvatar.ears === null || finalAvatar.head === null">
        Set avatar
      </button>
    </header>

    <main class="main">
      <h2>Create your Buidlbox avatar</h2>

      <output>
        <div :style="{ '--data-url': 'url(./src/assets/avatar/body/' + finalAvatar.body + ')' }" />
        <div :style="{ '--data-url': 'url(./src/assets/avatar/clothes/' + finalAvatar.clothes + ')' }" />
        <div :style="{ '--data-url': 'url(./src/assets/avatar/eyes/' + finalAvatar.eyes + ')' }" />
        <div :style="{ '--data-url': 'url(./src/assets/avatar/ears/' + finalAvatar.ears + ')' }" />
        <div :style="{ '--data-url': 'url(./src/assets/avatar/head/' + finalAvatar.head + ')' }" />
        <div :style="{ '--data-url': 'url(./src/assets/avatar/face/' + finalAvatar.face + ')' }" />
      </output>

      <ul>
        <li><button @click="finalAvatar.body = null, finalAvatar.clothes = null">reset</button></li>
        <li><button>random</button></li>
        <li><button>grayscale</button></li>
      </ul>
    </main>

    <footer class="footer">

      <div class="footer__tabs">
        <ul>
          <li><button @click="activeTab = 'body'" class="active">Body</button></li>
          <li><button @click="activeTab = 'head'">Head</button></li>
          <li><button @click="activeTab = 'face'">Face</button></li>
          <li><button @click="activeTab = 'eyes'">Eyes</button></li>
          <li><button @click="activeTab = 'ears'">Ears</button></li>
          <li><button @click="activeTab = 'clothes'">Clothes</button></li>
        </ul>
      </div>

      <div class="footer__content">
        <template v-if="activeTab === 'body'">
          <div v-for="(item, index) in AvatarDB.body" :key="index"
            @click="finalAvatar.body = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/body/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'head'">
          <div v-for="(item, index) in AvatarDB.head" :key="index"
            @click="finalAvatar.head = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/head/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'face'">
          <div v-for="(item, index) in AvatarDB.face" :key="index"
            @click="finalAvatar.face = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/face/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'ears'">
          <div v-for="(item, index) in AvatarDB.ears" :key="index"
            @click="finalAvatar.ears = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/ears/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'clothes'">
          <div v-for="(item, index) in AvatarDB.clothes" :key="index"
            @click="finalAvatar.clothes = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/clothes/' + item + ')' }" />
        </template>

        <template v-if="activeTab === 'eyes'">
          <div v-for="(item, index) in AvatarDB.eyes" :key="index"
            @click="finalAvatar.eyes = item; console.log(finalAvatar)"
            :style="{ '--data-url': 'url(./src/assets/avatar/eyes/' + item + ')' }" />
        </template>
      </div>

      <div class="footer__more">
        <small>
          No idea? <br />
          Try one of these
        </small>

        <figure>
          <img src="./../assets/logo.svg" />
          <img src="./../assets/logo.svg" />
          <img src="./../assets/logo.svg" />
          <img src="./../assets/logo.svg" />
          <img src="./../assets/logo.svg" />
          <img src="./../assets/logo.svg" />
        </figure>

        <button>View more</button>
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
  border-radius: 50px;
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

    >div {
      width: 100%;
      height: 100%;
      position: absolute;
      inset: 0;
      border-radius: inherit;
      background-image: var(--data-url);
      background-position: center;
    }
  }

  ul {
    display: flex;
    align-items: center;
    justify-content: space-around;
    column-gap: 1rem;

    li {
      button {
        background-color: var(--color-border);
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

  output {
    position: relative;
    --r: 32px;
    width: var(--r);
    height: var(--r);
    background-color: var(--color-black);
    border-radius: 999px;
    zoom: 6;
  }
}

.footer {
  background-color: var(--color-footer-background);
  border-radius: 40px;

  ul {
    display: flex;
  }

  &__tabs {
    padding: 1rem 1rem;
  }

  &__content {
    height: 200px;
    overflow-y: auto;
    color: #fff;
    padding: 1rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
    row-gap: 1rem;
    margin-bottom: 2rem;

    div {
      width: 32px;
      height: 32px;
      background-color: #1B374A;
      background-image: var(--data-url);
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
    color: #ACACAC
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