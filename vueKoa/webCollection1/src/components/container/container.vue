<template>
  <div class="page-container">
    <header-nav></header-nav>
    <router-view class="main-layout"></router-view>
  </div>
</template>

<script>
import headerNav from './header.vue'

export default {
  components: {
    headerNav
  }
}
</script>

<style>

.main-layout {
  padding-top: 10px;
}
</style>
