<template>
  <!-- 商品管理 -->
  <div class="goods">
  <el-row :gutter="20">
    <el-col :span="3">
      <ul class="aside-nav">
        <li><router-link to="/page/goods">web列表</router-link></li>
      </ul>
    </el-col>
    <el-col :span="21">
      <router-view></router-view>
    </el-col>
  </el-row>
  </div>
  <!-- <div style="width:20px">
    <router-link to="/page/goods">web列表</router-link>
  </div> -->
</template>
<style scoped>
@media screen and (max-width: 650px) {
  .aside-nav{
    display: none;
  }

}

</style>

