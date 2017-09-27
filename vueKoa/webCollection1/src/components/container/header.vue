<template>
  <div class="container">
    <div class="header navbar-top">
      <div class="header-item">

        <router-link to="/page/userHome">主页</router-link>
        <router-link to="/page/goods">地址管理</router-link>
        <router-link to="/page/platform">平台管理</router-link>
      </div>

      <div class="header-item">
        <strong>欢迎你，{{ name }}</strong>
        |
        <el-button type="text" @click="logout">退出</el-button>
      </div>

    </div>
    <el-menu default-active="2" class="el-menu-vertical-demo pc-hide">
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-message"></i>@lanll</template>
        <el-menu-item-group>
          <template slot="title">分组一</template>
          <el-menu-item index="1-0">
            <router-link to="/page/userHome">主页</router-link>
          </el-menu-item>
          <el-menu-item index="1-1">
            <router-link to="/page/goods">地址管理</router-link>
          </el-menu-item>
          <el-menu-item index="1-2">
            <router-link to="/page/platform">平台管理</router-link>
          </el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group title="分组2">
          <el-menu-item index="1-3">
            <el-button type="text" @click="logout">退出</el-button>

          </el-menu-item>
        </el-menu-item-group>
        <el-submenu index="1-4">
          <template slot="title">More</template>
          <el-menu-item index="1-4-1">More</el-menu-item>
        </el-submenu>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
import jwt from 'jsonwebtoken' // 安装koa-jwt的时候会自动下载这个依赖

export default {
  created() {
    this.name = this.getUserInfo() && this.getUserInfo().name || '';
  },
  methods: {
    getUserInfo() { // 获取用户信息
      const token = localStorage.getItem('demo-token');

      if (token != null && token != 'null') {
        const decode = jwt.verify(token, 'vue-koa-demo'); // 解析token

        return decode
      } else {
        return null
      }
    },
    logout() {
      localStorage.removeItem('demo-token');
      this.$router.push('/');
    }
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.42857143;
  color: #333;
}

button,
input,
optgroup,
select,
textarea {
  margin: 0;
  font: inherit;
}
</style>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

a {
  text-decoration: none;
  color:#20a0ff;
}



.navbar-top {
  width: 100%;
  height: 60px;
}

.header {
  background: lightgray;
}

.header-item {
  display: inline-block;
}

.header h1 {
  display: inline-block;
  margin: .5em 0 .5em 1em;
  font-size: 1.5rem;
  vertical-align: middle;
}

.header a {
  margin: 0 10px;
  color: #000;
  text-decoration: none;
  vertical-align: middle;
}
.router-link {
  color: #999;
}
.router-link-active {
  color: lightcoral;
}

.header strong {
  display: inline-block;
  margin-top: 1.3em;
}

.pc-hide {
  display: none;
}

@media screen and (max-width: 650px) {
  .header {
    display: none;
  }
  .pc-hide {
    display: block;
  }

}
</style>
