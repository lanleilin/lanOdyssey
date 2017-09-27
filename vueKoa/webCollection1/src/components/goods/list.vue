<template>
  <div class="container">
    
    <div class="banner">
      <ul>
        <li>
          <router-link to="/page/goods/management">
            <el-button type="primary">新增web</el-button>
          </router-link>
        </li>
        <li>
          <el-input placeholder="请输入web名称" size="small" icon="search" v-model="searchVal" @keyup.enter.native="handleSearch" :on-icon-click="handleSearch">
          </el-input>
        </li>
      </ul>

    </div>

    <el-table :data="list" border style="margin:10px 0;">
      <el-table-column prop="id" label="id">
      </el-table-column>
      <el-table-column prop="name" label="名称">
      </el-table-column>
      <el-table-column prop="description" label="描述">
      </el-table-column>
      <el-table-column label="前往">
        <template scope="scope">
          <el-button type="primary" size="small"  @click="testlog(scope.row.id)">GO</el-button>
            <a :href = scope.row.description target="_blank">前往</a>
        </template>
      </el-table-column>
      <el-table-column prop="img" label="图片">
        <template scope="scope">
          <img v-for="item in myScope[scope.row.id]" :key="item" :src="item">
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template scope="scope">
          <el-button type="primary" size="small" @click="toEdit(scope.row.id)">编辑</el-button>
          <el-button type="danger" size="small" @click="removeGoodsList(scope.row.id)">删除</el-button>
          <!-- <el-button type="primary" size="small">前往</el-button> -->
        </template>
      </el-table-column>
    </el-table>

    <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage" :page-sizes="[5, 6, 7, 8]" :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper" :total="total">
    </el-pagination>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      searchVal: '',
      list: [],
      myScope: {},
      currentPage: 1,
      pageSize: 2,
      total: 0
    }
  },
  created() {
    this.getGoodsList();
  },
  methods: {
    getGoodsList() {
      const that = this
      const currentPage = this.currentPage;
      const pageSize = this.pageSize;
      const goodsName = this.searchVal.replace(/^\s+|\s+$/g, '');

      this.searchVal = goodsName;

      return this.$http.post('/goods/list', {
        currentPage: currentPage,
        pageSize: pageSize,
        searchVal: goodsName
      })
        .then((response) => {
          this.loading = false;

          if (response.status == 200) {
            this.list = response.data.list;
            this.total = response.data.total;
            if (Array.isArray(this.list) && this.list.length) {
              this.list.forEach(function(item, index) {
                if (item.img_url) {
                  that.myScope[item.id] = item.img_url.split(';');
                }
              });
            }
          } else {
            this.$message.error('获取web列表失败！');
          }
        }, (error) => {
          this.loading = false;
          this.$message.error('网络错误！');
        });
    },
    toEdit(id) {
      this.$router.push('/page/goods/management/' + id);
    },
    removeGoodsList(id) {
      this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        return this.$http.delete('/goods/' + id)
          .then((response) => {
            if (response.status == 200) {
              this.getGoodsList();
              this.$message.success('删除成功！');
            } else {
              this.$message.error('删除失败！');
            }
          }, (error) => {
            this.$message.error('网络错误！');
          });
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        });
      });
    },
    handleSizeChange(size) {
      this.pageSize = size;
      this.getGoodsList();

      console.log(`每页 ${size} 条`);
    },
    handleCurrentChange(currentPage) {
      this.currentPage = currentPage;
      this.getGoodsList();

      console.log(`当前页: ${currentPage}`);
    },
    handleSearch(event) {
      this.getGoodsList();
    },
    testlog(id) {
      console.log('testlog');
      console.log(id)
      console.log(this.list)
      console.log(this.list[1].description)
      // window.location.href=this.list[1].description
    }
  }
}
</script>
<style>
.el-button--small {
  margin: 12px;
}

tbody {
  background: none;
}
</style>

<style scoped>
ul {
  width: 100vw;
  height: 50px;
  margin-bottom: 5px;
}

ul>li {
  list-style: none;
  width: 40vw;
  float: left;
}
</style>

