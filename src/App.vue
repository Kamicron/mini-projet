<template>
  <header>
    <nav class="header_menu">
      <ul class="header_menu-list">
        <li class="header_menu-item">
          <RouterLink to="/">Home</RouterLink>
        </li>
        <li class="header_menu-item">
          <RouterLink to="/about">About</RouterLink>
        </li>
      </ul>
      <transition name="fade">
        <ModeSwitcher />
      </transition>
    </nav>

    <RouterView />
  </header>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
import ModeSwitcher from './components/ModeSwitcher.vue';


export default {
  components: {
    RouterLink,
    RouterView,
    ModeSwitcher
  }
};

</script>

<style scoped>
.header_menu {
  background-color: var(--second-color);
}

.header_menu-list {
  display: flex;
  list-style-type: none;
  justify-content: right;
  margin: 0 10%;

}

.header_menu-item {
  padding: 10px;
  font-size: 1.5rem;
  color: var(--main-white_color);
}

a {
  text-decoration: none;
  color: var(--main-white_color);
  position: relative;
}

a::after {
  content: "";
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 4px;
  background-color: var(--dynamic-color);
  transition: width .3s ease;
}

a:hover::after {
  width: 100%;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
