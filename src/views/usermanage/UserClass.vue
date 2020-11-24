<template>
  <!-- 用户分类 -->
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="classform" class="demo-form-inline">
          <el-form-item label="昵称:">
            <el-input v-model="name" placeholder="请输入昵称" />
          </el-form-item>
          <el-form-item label="用户ID:">
            <el-input v-model="id" placeholder="请输入ID" />
          </el-form-item>
          <el-form-item label="手机号:">
            <el-input v-model="phone" placeholder="请输入手机号" />
          </el-form-item>
          <el-form-item label="流失天数:">
            <el-input v-model="day" />
          </el-form-item>
          <el-form-item label="消费状态:">
            <el-input v-model="state" />
          </el-form-item>
          <el-form-item label="用户属性:">
            <el-input v-model="attribute" />
          </el-form-item>
          <el-form-item>
            <el-button type="primary">开始查询</el-button>
          </el-form-item>
          <el-form-item>
            <el-button type="danger">导出表格</el-button>
          </el-form-item>
        </el-form>
      </div>
      <!-- 表格 -->
      <el-table :data="userClassData" border style="width: 100%" class="table">
        <el-table-column prop="name" label="昵称" align="center" />
        <el-table-column prop="userid" label="用户ID" align="center" />
        <el-table-column
          prop="phone"
          label="手机号"
          align="center"
        />
        <el-table-column
          prop="date"
          label="注册时间"
          width="200"
          align="center"
        />
        <el-table-column prop="headImg" label="用户头像" align="center" />
        <el-table-column prop="sex" label="性别" align="center" />
        <el-table-column prop="userState" label="用户状态" align="center" />
        <el-table-column prop="lossday" label="流失天数" align="center" />
        <el-table-column prop="conState" label="消费状态" align="center" />
        <el-table-column prop="userAttribute" label="用户属性" align="center" />
        <el-table-column prop="bindGuild" label="绑定公会" align="center" />
        <el-table-column prop="account" label="账户余额" align="center" />
        <el-table-column prop="activeState" label="活跃状态" align="center" />
        <el-table-column prop="loginIP" label="登录IP" align="center" />
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
      // 头部搜索
      classform: {
        name: '',
        id: '',
        day: '',
        phone: '',
        state: '',
        attribute: ''
      },
      //   表格数据
      userClassData: [
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        },
        {
          name: '张三',
          userid: '001',
          phone: 1518221232,
          date: '2020-10-12 10:40:32',
          headImg: '',
          sex: '男',
          userState: '老用户',
          lossday: 5,
          conState: '已消费',
          userAttribute: '大神',
          bindGuild: 60551,
          account: 20000,
          activeState: '活跃',
          loginIP: '556.665.556'
        }
      ]
    }
  },
  methods: {
    // 分页
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
.el-form-item {
  margin-right: 50px;
}
</style>
