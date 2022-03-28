<script>
import { RouterLink, RouterView } from 'vue-router';

export default {
  name: '#app',
};
</script>

<template :id="app">
  <div>
    <header>
      <div class="leftHeader">
        <nav>
          <RouterLink to="/"
            ><img
              src="https://upload.wikimedia.org/wikipedia/commons/c/c4/Decathlon_Logo.svg"
              alt="decathlon"
          /></RouterLink>
          <!-- <RouterLink to="/about">About</RouterLink>  -->
        </nav>
      </div>
    </header>

    <RouterView />
    <footer></footer>
  </div>
</template>

<style>
@import '@/assets/base.scss';
</style>
