<script setup>
import { ref } from "vue";

const items = [
  {
    main: "Umiejętności",
    subMenu: ["JavaScript", "React", "HTML & CSS"],
    id: 1,
  },
  {
    main: "Wykształcenie",
    subMenu: ["Uniwersytet Warszawski", "Politechnika Warszawska"],
    id: 2,
  },
  {
    main: "Hobby",
    subMenu: [
      "Wioślarstwo",
      "Uprawa warzyw i ziół",
      "Pieczenie chleba na zakwasie",
    ],
    id: 3,
  },
  {
    main: "Kontakt",
    subMenu: ["789 - 345 - 117"],
    id: 4,
  },
];

const isOpen = ref(false);

const activeItem = ref(null);

const showMenu = () => {
  isOpen.value = !isOpen.value;
  activeItem.value = null;
};

const setActiveItem = (item) => {
  if (activeItem.value === item.id) {
    activeItem.value = null;
  } else {
    activeItem.value = item.id;
  }
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
      <ul>
        <li
          v-for="item in items"
          class="item"
          :class="{ active: item.id === activeItem }"
          @click="setActiveItem(item)"
          :key="item.id"
        >
          <span>
            {{ item.main }}
          </span>
          <transition name="subMenu" mode="in-out">
            <ul v-if="item.id === activeItem">
              <li
                v-for="subitem in item.subMenu"
                class="subitem"
                :key="subitem"
              >
                {{ subitem }}
              </li>
            </ul>
          </transition>
        </li>
      </ul>
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
  min-height: 100%;
  width: 300px;
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
  display: block;
  width: 100%;

  margin: 0 auto 16px;
  padding: 8px 12px;
  transition: 0.4s;
}

.menu .item span {
  cursor: pointer;
  display: block;
  padding: 8px 12px;
  transition: 0.2s;
}

.menu .item span:hover {
  background-color: var(--color-background-soft);
  border-radius: 4px;
}

.menu .item.active span {
  font-weight: bold;
  font-size: 22px;
}
.menu .item .subitem {
  margin: 0 8px;
  padding: 12px 12px;
  transition: 0.4s;
}

.subMenu-enter-active {
  transition: all 0.3s ease;
}
.subMenu-enter,
.subMenu-leave-to {
  opacity: 0;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

ul li span {
  font-size: 20px;
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
</style>
