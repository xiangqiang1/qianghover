<template>
  <div>
    <!-- 头部表单 -->
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="BanUesrsData" class="formData">
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
          <el-form-item label="审核类别:">
            <el-select v-model="BanUesrsData.category" placeholder="请选择类别">
              <el-option
                v-for="item in BanUesrsData.option1"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="审核状态:">
            <el-select v-model="BanUesrsData.state" placeholder="请选择状态">
              <el-option
                v-for="item in BanUesrsData.option2"
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
        <el-table-column prop="name" label="用户id" align="center" />
        <el-table-column prop="address" label="头像缩略图" align="center" />
        <el-table-column prop="address" label="背景缩略图" align="center" />
        <el-table-column prop="address" label="相册图片" align="center" />
        <el-table-column prop="address" label="主播欢迎语" align="center" />
        <el-table-column prop="address" label="更新时间" align="center" />
        <el-table-column prop="address" label="审核状态" align="center" />
        <template>
          <el-table-column
            prop="address"
            label="操作"
            width="350px"
            align="center"
          >
            <el-button type="success" @click="AllPassed">全部通过</el-button>
            <el-button type="danger" @click="AllReject">全部拒绝</el-button>
            <el-button
              type="warning"
              @click="dialogFormVisible = true"
            >部分拒绝</el-button>
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
      <!-- 部分审核拒绝的模态框 -->
      <el-dialog
        title="部分素材审核拒绝"
        :visible.sync="dialogFormVisible"
        center
        width="30%"
      >
        <div>
          <el-checkbox-group v-model="SelectChenckList">
            <el-checkbox
              v-for="item in checkList"
              :key="item"
              :label="item"
            />
          </el-checkbox-group>
        </div>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button
            type="primary"
            @click="dialogFormVisible = false"
          >确 定</el-button>
        </div>
      </el-dialog>
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
        state: '', // 审核状态
        category: '', // 审核类别
        option1: ['头像', '房间封面图', '房间背景图', '相册图', '欢迎语'],
        option2: ['全部通过', '全部拒绝', '部分拒绝']
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
      ],
      formLabelWidth: '120px',
      dialogFormVisible: false, // 部分审核拒绝
      SelectChenckList: [], // 选中的数组
      checkList: ['头像', '房间封面页', '房间背景图', '相册图', '欢迎语'] // 循环的数组
    }
  },
  methods: {
    //   全部拒绝
    AllReject() {
      this.$confirm('您确定要全部拒绝吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '拒绝成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消拒绝！'
          })
        })
    },
    //   全部通过
    AllPassed() {
      this.$confirm('您确定要全部通过吗?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.$message({
            type: 'success',
            message: '通过成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '已取消通过!'
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
.input {
  width: 400px;
}
.formData {
  .el-form-item {
    margin-right: 20px;
  }
  .el-input,
  .el-select {
    width: 160px;
  }
}
</style>
