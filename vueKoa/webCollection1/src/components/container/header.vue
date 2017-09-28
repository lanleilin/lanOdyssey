<template>
  <div class="container">
    <div class="header navbar-top">
      <div class="header-item" id="item">
        <router-link to="/page/userHome">主页</router-link>
        <router-link to="/page/goods">地址管理</router-link>
        <router-link to="/page/platform">平台管理</router-link>
        <router-link to="/page/dashboard">dashboard</router-link>
      </div>
      <div class="header-item" id="logout">
        <strong>欢迎你，{{ name }}</strong>
        |
        <el-button type="text" @click="logout">退出</el-button>
      </div>
    </div>
    <el-menu default-active="2" class="el-menu-vertical-demo pc-hide">
      <el-submenu index="1">
        <template slot="title">
          <!-- <img class="logo" src="../../assets/img/doge.svg" alt="logo"> -->
          <img class="logo" :src="logoUrl" alt="logo"> @lanll
        </template>
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
            <router-link to="/page/dashboard">dashboard</router-link>
          </el-menu-item>
        </el-menu-item-group>
        <el-submenu index="1-4">
          <template slot="title">More</template>
          <el-menu-item index="1-4-1">
            <el-button type="text" @click="logout">退出</el-button>
          </el-menu-item>
        </el-submenu>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
import jwt from 'jsonwebtoken' // 安装koa-jwt的时候会自动下载这个依赖

export default {
  data() {
    return {
      logoUrl: require("../../assets/img/doge.svg")
    }
  },
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

.el-button--text {
  color: #97a8be;
}

.router-link-active {
  color: lightcoral;
}
</style>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

a {
  text-decoration: none;
  color: #97a8be;
}

.container {
  position: fixed;
  width: 100%;
  z-index: 9999;
}

.navbar-top {
  width: 100%;
  height: 60px;
}

.header {
  background: lightgray;
  padding: 0 50px;
  box-sizing: border-box;
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
  .logo {
    width: 40px;
  }
}

#logout {
  float: right;
}

#item {
  float: left;
  margin-top: 1.3em;
}
</style>
