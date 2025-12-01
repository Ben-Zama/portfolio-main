<template>
  <div class="header" :class="{ opened: menuOpen }">
    <header>
      <h2>Benzama</h2>
      <Hamburger :open="menuOpen" @toggle="menuOpen = !menuOpen" />
    </header>
    <nav>
      <a href="#">Home</a>
      <a href="#">About me</a>
      <a href="#">Services</a>
      <a href="#">Portfolio</a>
      <a href="#">Contact me</a>
      <hr>
      <div class="social">
        <a href="#" target="_blank">
          <PhGithubLogo :size="28" weight="bold" />
        </a>
        <a href="#" target="_blank">
          <PhLinkedinLogo :size="28" weight="bold" />
        </a>
        <a href="#" target="_blank">
          <PhXLogo :size="28" weight="bold" />
        </a>
        <a href="#" target="_blank">
          <PhInstagramLogo :size="28" weight="bold" />
        </a>
      </div>
    </nav>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Hamburger from "./hamburger.vue";
import {
  PhGithubLogo,
  PhInstagramLogo,
  PhLinkedinLogo,
  PhXLogo,
} from "@phosphor-icons/vue";

const menuOpen = ref(false);

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};
</script>

<style lang="scss" scoped>
.header {
  position: absolute;
  top: 15px;
  left: 15px;
  z-index: 5;
  padding: 15px 20px;
  width: 250px;
  background: var(--translucent-primary);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  display: flex;
  flex-direction: column;
  border-radius: 32px;
  transition: 0.3s;
  &.opened {
    width: 300px;
    nav {
      margin-top: 25px;
      height: 400px;
    }
  }
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    h2 {
      font-family: var(--logo-font);
      font-weight: 800;
      font-size: 20px;
      color: var(--secondary);
    }
  }
  nav {
    margin-top: 0;
    height: 0;
    display: flex;
    flex-direction: column;
    gap: 25px;
    overflow: hidden;
    transition: 0.3s;
    > a {
      width: max-content;
      font-family: var(--alternate-font);
      font-size: 32px;
      color: var(--secondary);
      transition: 0.3s;
      &:hover {
        padding-left: 5px;
        color: var(--accent);
      }
    }
    hr {
      border: 1px solid var(--translucent-secondary);
      border-radius: 8px;
    }
    .social {
      display: flex;
      gap: 15px;
      svg {
        color: var(--secondary);
        &:hover {
        color: var(--accent);
        }
      }
    }
  }
}

@media (min-width: 600px) {
  .header {
    top: 25px;
    left: 25px;
  }
}
</style>