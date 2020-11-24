<template>
  <div>
    <!-- 头部表单 -->
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="BanUesrsData" class="demo-form-inline">
          <el-form-item label="昵称:">
            <el-input
              v-model="BanUesrsData.nickname"
              placeholder="请输入昵称"
            />
          </el-form-item>
          <el-form-item label="用户ID:">
            <el-input
              v-model="BanUesrsData.userId"
              placeholder="请输入用户ID"
            />
          </el-form-item>
          <el-form-item label="公会ID:">
            <el-input
              v-model="BanUesrsData.GuildID"
              placeholder="请输入用户ID"
            />
          </el-form-item>
          <el-form-item label="状态:">
            <el-select v-model="BanUesrsData.state" placeholder="请选择状态">
              <el-option
                v-for="item in BanUesrsData.option"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">开始查询</el-button>
            <el-button type="danger">导出表格</el-button>
          </el-form-item>
        </el-form>
      </div>
      <!--表格-->
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="date" label="昵称" align="center" />
        <el-table-column prop="name" label="用户ID" align="center" />
        <el-table-column prop="address" label="注册时间" align="center" />
        <el-table-column prop="address" label="用户头像" align="center" />
        <el-table-column prop="address" label="性别" align="center" />
        <el-table-column prop="address" label="状态" align="center" />
        <el-table-column prop="address" label="绑定公会" align="center" />
        <el-table-column prop="address" label="账户余额" align="center" />
        <el-table-column prop="address" label="登录IP" align="center" />
        <template>
          <el-table-column
            prop="address"
            label="操作"
            width="250px"
            align="center"
          >
            <el-button
              type="success"
              @click="SetUnsealUser"
            >解除账号</el-button>
            <el-button type="danger" @click="SetBanusers">封禁账号</el-button>
          </el-table-column>
        </template>
      </el-table>
      <!-- 分页 -->
      <div class="pagination">
        <el-pagination
          :current-page="1"
          :page-sizes="[100, 200, 300, 400]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="400"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
        />
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      BanUesrsData: {
        nickname: '',
        userId: '',
        GuildID: '',
        state: '',
        option: ['已封禁', '正常']
      },
      //   表格数据
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }
      ]
    }
  },
  methods: {
    //   确认封禁
    SetBanusers() {
      this.$confirm('您确定要封禁该用户吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '封禁成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消封禁'
          })
        })
    },
    //   确认解封
    SetUnsealUser() {
      this.$confirm('您确定要解除封禁该用户吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '解封成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '解封失败!'
          })
        })
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    }
  }
}
</script>

<style lang="scss" scoped>
.dialogCenter {
  text-align: center;
  span {
    font-size: 18px;
    font-weight: bold;
  }
}
</style>
