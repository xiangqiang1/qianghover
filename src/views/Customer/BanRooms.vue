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
        <el-table-column prop="date" label="注册时间" align="center" />
        <el-table-column prop="name" label="房间号" align="center" />
        <el-table-column prop="address" label="房间名字" align="center" />
        <el-table-column prop="address" label="房间封面" align="center" />
        <el-table-column prop="address" label="状态" align="center" />
        <el-table-column prop="address" label="绑定公会" align="center" />
        <el-table-column prop="address" label="登录IP" align="center" />
        <template>
          <el-table-column
            prop="address"
            label="操作"
            width="350px"
            align="center"
          >
            <el-button type="success" @click="UnsealRoom">解除房间</el-button>
            <el-button
              type="warning"
              @click="RectRoom = true"
            >整改房间</el-button>
            <el-button type="danger" @click="ClosedRoom">封禁房间</el-button>
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
      <!-- 整改房间的模态框 -->
      <el-dialog title="整改房间" :visible.sync="RectRoom" center width="30%">
        <el-form :model="formData">
          <el-form-item label="整改时间" :label-width="formLabelWidth">
            <el-date-picker
              v-model="formData.RectTime"
              type="datetimerange"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
            />
          </el-form-item>
          <el-form-item label="整改理由" :label-width="formLabelWidth">
            <el-input
              v-model="formData.reason"
              autocomplete="off"
              class="input"
            />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="RectRoom = false">取 消</el-button>
          <el-button type="primary" @click="RectRoom = false">确 定</el-button>
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
      ],
      formLabelWidth: '120px',
      RectRoom: false, // 整改房间
      formData: {
        reason: '',
        RectTime: [] // 整改时间
      }
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
    }
  }
}
</script>

<style lang="scss" scoped>
.input {
  width: 400px;
}
</style>
