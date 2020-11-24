<template>
  <div>
    <!-- 头部表单 -->
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="SquareData" class="forData">
          <el-form-item label="发布时间:">
            <el-date-picker
              v-model="SquareData.ReleaseTime"
              type="datetimerange"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
            />
          </el-form-item>
          <el-form-item label="用户ID:">
            <el-input
              v-model="SquareData.userId"
              placeholder="请输入用户ID"
            />
          </el-form-item>
          <el-form-item label="话题选择:">
            <el-input
              v-model="SquareData.topicSel"
              placeholder="请输入话题"
            />
          </el-form-item>
          <el-form-item label="动态类型:">
            <el-input
              v-model="SquareData.Dytype"
              placeholder="请输入类型"
            />
          </el-form-item>
          <el-form-item label="发布状态:">
            <el-input
              v-model="SquareData.state"
              placeholder="请输入状态"
            />
          </el-form-item>
          <el-form-item>
            <el-button type="primary">开始查询</el-button>
            <el-button type="danger">导出表格</el-button>
          </el-form-item>
        </el-form>
      </div>
      <!--表格-->
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="date" label="发布时间" align="center" />
        <el-table-column prop="name" label="用户ID" align="center" />
        <el-table-column prop="address" label="用户昵称" align="center" />
        <el-table-column prop="address" label="话题名称" align="center" />
        <el-table-column prop="address" label="文字" align="center" />
        <el-table-column prop="address" label="图片" align="center" />
        <el-table-column prop="address" label="音频" align="center" />
        <el-table-column prop="address" label="浏览数量" align="center" />
        <el-table-column prop="address" label="点赞数量" align="center" />
        <el-table-column prop="address" label="评论数量" align="center">
          <template>
            <div>9</div>
            <el-button
              type="primary"
              @click="dialogFormVisible = true"
            >查看</el-button>
          </template>
        </el-table-column>
        <el-table-column
          prop="address"
          label="发布状态"
          align="center"
        >拒绝
        </el-table-column>
        <template>
          <el-table-column
            prop="address"
            label="操作"
            width="250px"
            align="center"
          >
            <el-button type="success" @click="UnsealRoom">通过</el-button>
            <el-button type="danger" @click="ClosedRoom">拒绝</el-button>
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
      <!-- 查看评论的模态框 -->
      <el-dialog
        title="评论管理"
        :visible.sync="dialogFormVisible"
        center
        width="35%"
      >
        <div class="main">
          <div class="dialogMain">
            <img
              src="../../assets/401_images/u=2233854763,678386514&fm=11&gp=0.jpg"
              alt=""
            >
            <div>
              小强评论说：你太牛b了11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111
            </div>
            <el-button type="primary" @click="spliceText">删除评论</el-button>
          </div>
          <div class="dialogMain">
            <img
              src="../../assets/401_images/u=2233854763,678386514&fm=11&gp=0.jpg"
              alt=""
            >
            <div>
              小强评论说：你太牛b了11111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111
            </div>
            <el-button type="primary" @click="spliceText">删除评论</el-button>
          </div>
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
      SquareData: {
        ReleaseTime: [],
        userId: '',
        topicSel: '',
        state: '',
        Dytype: ''
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
      dialogFormVisible: false // 评论管理
    }
  },
  methods: {
    //   封禁房间
    ClosedRoom() {
      this.$confirm('您确定要封禁该房间吗?', '提示', {
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
    //   解封房间
    UnsealRoom() {
      this.$confirm('您确定要解除封禁该房间吗?', '提示', {
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
    },
    // 删除评论
    spliceText() {
      this.$confirm('您确定删除这条评论吗?', '提示', {
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
.input {
  width: 400px;
}
.forData .el-form-item {
  margin-right: 75px;
}
// 查看评论的样式
.main{
  width: 100%;
  height: 400px;
  overflow: auto;
}
.dialogMain {
  margin-bottom:10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  div {
    flex: 1;
    margin: 0px 15px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .el-button{
    margin-right: 15px;
  }
  img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
}
</style>
