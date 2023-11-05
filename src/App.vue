<script setup>
import AvatarBuilder from './components/AvatarBuilder.vue'
import IconAvatar from './components/icons/IconAvatar.vue' 
</script>

<template>
  <template v-if="showAvatarModal === false">
    <div class="profile">
      <span>
        Profile avatar
      </span>
      <figure>
        <IconAvatar/>
      </figure>
      <ul>
        <li><button>Choose file</button></li>
        <li><button @click="avatarModal()">Try avatar builder</button></li>
        <li><button>Delete my avatar</button></li>
      </ul>
    </div>
  </template>

  <template v-if="showAvatarModal === true">
    <AvatarBuilder />
  </template>
</template>

<style lang="scss" scoped>
.profile {
  width: 600px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 1rem;
  background-color: #1B374A;

  svg {
    width: 120px;
  }

  ul {
    display: flex;
    flex-direction: column;
    row-gap: 1rem;

    li {
      color: var(--white);
      display: flex;
      border-radius: 4px;

      &:not(:nth-child(3)) {
        border: 1px solid var(--color-text);
      }

      &:nth-child(3) {
        border: 1px solid var(--destructive);
        opacity: .8;

        button {
          color: var(--destructive);
        }
      }

      button {
        width: 100%;
        all: unset;
        padding: .2rem .4rem;
        cursor: pointer;
      }
    }
  }
}
</style>

<script>
export default {
  data() {
    return {
      showAvatarModal: false
    }
  },
  methods: {
    avatarModal() {
      this.showAvatarModal = !this.showAvatarModal
    },

  },
}
</script>