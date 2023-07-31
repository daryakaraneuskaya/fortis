<script setup>
import { ref } from "vue";

const isOpen = ref(false);

const showMenu = () => {
  isOpen.value = !isOpen.value;
};
</script>

<template>
  <div class="home">
    <nav class="nav-bar">
      <div class="menu-burger" @click="showMenu">
        <svg
          v-if="!isOpen"
          xmlns="http://www.w3.org/2000/svg"
          width="32"
          height="32"
          fill="#000000"
          viewBox="0 0 256 256"
        >
          <path
            d="M224,128a8,8,0,0,1-8,8H40a8,8,0,0,1,0-16H216A8,8,0,0,1,224,128ZM40,72H216a8,8,0,0,0,0-16H40a8,8,0,0,0,0,16ZM216,184H40a8,8,0,0,0,0,16H216a8,8,0,0,0,0-16Z"
          ></path>
        </svg>
        <svg
          v-else
          xmlns="http://www.w3.org/2000/svg"
          width="32"
          height="32"
          fill="#000000"
          viewBox="0 0 256 256"
        >
          <path
            d="M205.66,194.34a8,8,0,0,1-11.32,11.32L128,139.31,61.66,205.66a8,8,0,0,1-11.32-11.32L116.69,128,50.34,61.66A8,8,0,0,1,61.66,50.34L128,116.69l66.34-66.35a8,8,0,0,1,11.32,11.32L139.31,128Z"
          ></path>
        </svg>
      </div>
    </nav>
    <section class="menu" :class="{ active: isOpen, closed: !isOpen }">
      <div class="item">
        <h3>Doświadczenie</h3>
      </div>
      <div class="item">
        <h3>Wykształcenie</h3>
      </div>
      <div class="item">
        <h3>Hobby</h3>
      </div>
      <div class="item">
        <h3>Kontakt</h3>
      </div>
    </section>
    <section class="hero">
      <div class="text">
        <h3>Darya Nowak</h3>
        <hr />
        <h2>Zadanie Rekrutacyjne</h2>
      </div>
    </section>
  </div>
</template>

<style scoped>
#app {
}
.home {
  position: relative;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.nav-bar {
  display: flex;
  height: 100px;
  padding: 12px;
}

.menu-burger {
  position: relative;
  display: flex;
  align-items: center;
  cursor: pointer;
  z-index: 2;
}
.menu-burger::after {
  content: "";
  height: 40px;
  width: 40px;
  border-radius: 50%;
  background-color: #f3f4f6;
  position: absolute;
  left: -4px;
  /* top: -4px;
  left: -4px; */
  /* transform: translateX(-50%); */
  opacity: 0;
  transition: opacity 0.3s ease;
}

.menu-burger:hover::after {
  opacity: 1;
  z-index: -1;
}
.menu {
  position: absolute;
  top: 0;
  left: -300px;
  /* margin-right: 100%; */
  min-height: 100%;
  width: 300px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  background-color: #fff;
  box-shadow: 18px 1px 24px -12px rgba(231, 231, 231, 1);
  padding-top: 100px;
  opacity: 0;
  transition: 0.8s ease-in-out;
}

.menu.active {
  left: 0;
  opacity: 1;
}

.menu .item {
  cursor: pointer;
  padding-left: 12px;
}
.hero {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}
.hero .text {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (max-width: 1024px) {
  .menu.active {
    /* width: 100%; */
  }
}

/* @media (min-width: 1024px) {
  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
} */
</style>
