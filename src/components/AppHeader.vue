<script>
export default {
  data() {
    return { 
      message: 'Laravel Boolfolio - API'
    }
  }
}
</script>

<template>
  <header>

    <ul class="nav nav-pills justify-content-center">
      <li class="nav-item">
        <router-link :to="{ name: 'home' }" class="nav-link">
          HOME
        </router-link>
      </li>
      <li class="nav-item">
        <router-link :to="{ name: 'about' }" class="nav-link">
          CHI SIAMO
        </router-link>
      </li>
      <li class="nav-item">
        <router-link :to="{ name: 'projects' }" class="nav-link">
          PROGETTI
        </router-link>
      </li>
    </ul>
  </header>
</template>

<style lang="scss" scoped>
@use '../assets/scss/partials/variables' as *;

header {
  background-color: $mainBgColor;
  text-align: center;
  padding: 20px 0;
}

h1 {
  color: $mainColor;
}
</style>
