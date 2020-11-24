<template>
  <!-- 广场话题列表 -->
  <div>
    <el-card class="box-card">
      <!-- 头部表单 -->
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="Squareform" class="demo-form-inline">
          <el-form-item label="创建者用户ID:">
            <el-input
              v-model="Squareform.creatorId"
              placeholder="请输入创建者用户ID"
            />
          </el-form-item>
          <el-form-item label="选择话题:">
            <el-select v-model="Squareform.topic" placeholder="请选择话题">
              <el-option
                v-for="item in Squareform.option"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="审核状态:">
            <el-select v-model="Squareform.state" placeholder="请选择状态">
              <el-option
                v-for="item in Squareform.option1"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">开始查询</el-button>
          </el-form-item>
        </el-form>
      </div>
      <!--表格-->
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="date" label="序号" align="center" />
        <el-table-column
          prop="name"
          label="创建者用户ID"
          align="center"
        />
        <el-table-column prop="address" label="话题名称" align="center" />
        <el-table-column prop="address" label="审核状态" align="center">
          <template>
            <el-button type="success" @click="success">通过</el-button>
            <el-button type="danger" @click="splice">删除</el-button>
          </template>
        </el-table-column>
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
      Squareform: {
        creatorId: '',
        topic: '',
        state: '',
        option: ['个人主页', '朋友圈'],
        option1: ['通过', '删除']
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
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    },
    // 通过
    success() {
      this.$confirm('您确定要通过吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '成功通过!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消通过'
          })
        })
    },
    // 删除
    splice() {
      this.$confirm('您确定要删除吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          })
        })
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
