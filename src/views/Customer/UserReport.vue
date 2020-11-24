<template>
  <!-- 用户举报查询 -->
  <div>
    <el-card class="box-card">
      <!-- 头部表单 -->
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="UesrsReport" class="demo-form-inline">
          <el-form-item label="举报ID:">
            <el-input
              v-model="UesrsReport.reportId"
              placeholder="请输入举报ID"
            />
          </el-form-item>
          <el-form-item label="被举报ID:">
            <el-input
              v-model="UesrsReport.BeireportId"
              placeholder="请输入被举报ID"
            />
          </el-form-item>
          <el-form-item label="举报来源:">
            <el-select v-model="UesrsReport.source" placeholder="请选择来源">
              <el-option
                v-for="item in UesrsReport.option"
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
        <el-table-column prop="date" label="举报时间" align="center" />
        <el-table-column prop="name" label="举报用户ID" align="center" />
        <el-table-column prop="address" label="被举报用户ID" align="center" />
        <el-table-column prop="address" label="举报来源" align="center" />
        <el-table-column prop="address" label="举报类型" align="center" />
        <el-table-column prop="address" label="举报内容" align="center" />
        <el-table-column
          prop="address"
          label="上传凭证"
          width="400px"
          align="center"
        />
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
      UesrsReport: {
        reportId: '',
        BeireportId: '',
        source: '',
        option: ['个人主页', '朋友圈']
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
