<template>
  <div>
    <!-- 用户日志 -->
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="Logform" class="demo-form-inline">
          <el-form-item label="昵称:">
            <el-input
              v-model="Logform.name"
              placeholder="请输入昵称"
            />
          </el-form-item>
          <el-form-item label="用户ID:">
            <el-input v-model="Logform.id" placeholder="请输入ID" />
          </el-form-item>
          <el-form-item label="手机号:">
            <el-input
              v-model="Logform.phone"
              placeholder="请输入手机号"
            />
          </el-form-item>
          <el-form-item label="操作内容">
            <el-input
              v-model="Logform.logtext"
              placeholder="请输入内容"
            />
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
      <el-table :data="userlogData" border style="width: 100%">
        <el-table-column prop="time" label="日期" width="180" align="center" />
        <el-table-column prop="name" label="姓名" width="180" align="center" />
        <el-table-column prop="userID" label="用户ID" width="180" align="center" />
        <el-table-column prop="userNum" label="手机号" width="180" align="center" />
        <el-table-column prop="userInfo" label="操作内容" align="center" />
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
      // 表头数据
      Logform: {
        name: '',
        id: '',
        phone: '',
        logtext: ''
      },
      // 表格数据
      userlogData: [
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        },
        {
          time: '2020-10-26 15:22:56',
          name: '张无忌',
          userID: 200,
          userNum: 15812322123,
          userInfo: '开了一会直播'
        }
      ]
    }
  }
}
</script>

<style scoped  lang='scss'>

</style>
