<template>
  <!-- 平台管理 -->
  <div class="container">

    <ul class="aside-nav">
      <li>
        <router-link to="/page/platform/userList">用户列表</router-link>
      </li>
      <li>
        <router-link to="/page/platform/rightsManagement">权限管理</router-link>
      </li>
    </ul>

    <router-view></router-view>

  </div>
</template>

 <style scoped>
.aside-nav {
  list-style: none;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: 0;
  background-color: rgba(0, 0, 0, .05);
}

.aside-nav a {
  display: block;
  padding: 10px 0;
  color: #555;
  text-align: center;
  text-decoration: none;
}

.aside-nav .router-link-active {
  color: #fff;
  background-color: orange;
}

.aside-nav {
  max-width: 500px;
}

.el-table {
  max-width: 500px;
  border: none;
}
</style>
