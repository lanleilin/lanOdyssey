<template>
  <!-- 商品管理 -->
  <div class="goods">
    <div class="list">
    <router-link to="/page/goods">web列表</router-link>
    </div>

    <router-view></router-view>

  </div>
</template>
<style scoped>
.list{
  width: 100vw;
  /* background:lightcoral; */
  height: 36px;
  display:table-cell;
  vertical-align: middle;
  padding-left: 5vw;
  border-bottom: 1px solid cadetblue;
  border-radius: 5px;
}
.list>a{
  text-decoration: none;
  color: cadetblue;
}
@media screen and (max-width: 650px) {
  /* .aside-nav{
    display: none;
  } */
}
</style>

