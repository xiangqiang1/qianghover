
<template>
  <div>
    <el-card class="box-card">
      <el-form
        ref="queryForm"
        :inline="true"
        label-position="center"
        label-width="75px"
        :model="UserInfo"
      >
        <el-form-item label="注册时间:" prop="jobName">
          <el-date-picker
            v-model="UserInfo.valuetime"
            type="datetimerange"
            :picker-options="pickerOptions"
            range-separator="至"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            align="right"
          />
        </el-form-item>
        <el-form-item label="昵称:">
          <el-input
            v-model="UserInfo.nickName"
            placeholder="请输入昵称"
            size="small"
          />
        </el-form-item>
        <el-form-item label="用户ID:">
          <el-input
            v-model="UserInfo.userId"
            placeholder="请输入用户ID"
            size="small"
          />
        </el-form-item>
        <el-form-item label="手机号:">
          <el-input
            v-model="UserInfo.phone"
            placeholder="请输入手机号"
            size="small"
          />
        </el-form-item>
        <el-form-item label="注册渠道:">
          <el-input
            v-model="UserInfo.reg"
            placeholder="请输入注册渠道"
          />
        </el-form-item>
        <el-form-item label="注册平台:">
          <el-select v-model="UserInfo.platform" placeholder="所有">
            <el-option label="安卓" value="安卓" />
            <el-option label="ios" value="ios" />
          </el-select>
        </el-form-item>
        <el-form-item label="身份证号:">
          <el-input
            v-model="UserInfo.ID"
            placeholder="请输入身份证号码"
          />
        </el-form-item>
        <el-form-item>
          <el-button type="primary" size="mini">开始查询</el-button>
          <el-button size="mini" type="danger">导出表格</el-button>
        </el-form-item>
      </el-form>

      <el-table :data="tableData" border style="width: 100%">
        <el-table-column fixed prop="date" label="昵称" width="150" />
        <el-table-column prop="name" label="用户ID" width="120" />
        <el-table-column prop="province" label="手机号" width="120" />
        <el-table-column prop="city" label="注册时间" width="120" />
        <el-table-column prop="address" label="用户头像" width="300" />
        <el-table-column prop="zip" label="性别" width="120" />
        <el-table-column prop="zip" label="注册渠道" width="120" />
        <el-table-column prop="zip" label="注册地区" width="120" />
        <el-table-column prop="zip" label="身份证号" width="120" />
        <el-table-column prop="zip" label="注册平台" width="120" />
        <el-table-column prop="zip" label="使用机型" width="120" />
        <el-table-column prop="zip" label="绑定公会" width="120" />
        <el-table-column prop="zip" label="账户余额" width="120" />
        <el-table-column prop="zip" label="活跃状态" width="120" />
        <el-table-column prop="zip" label="登录ip" width="120" />
        <el-table-column fixed="right" label="其他" width="100">
          <el-button
            type="primary"
            size="small"
            @click="opendialong"
          >编辑</el-button>
        </el-table-column>
      </el-table>
      <!-- 分页 -->
      <div class="pagination">
        <el-pagination
          :current-page="1"
          :page-sizes="[30, 40, 60, 80]"
          :page-size="30"
          layout="total, sizes, prev, pager, next, jumper"
          :total="400"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
        />
      </div>
      <!-- 编辑的模态框 -->
      <el-dialog
        title="编辑页面"
        :visible.sync="dialogFormVisible"
        center
        width="30%"
      >
        <el-form :model="formBasic">
          <el-form-item label="重置密码" :label-width="formLabelWidth">
            <el-button type="danger" plain>重置密码</el-button>
            <div class="iptBox">
              <span>系统密码:</span>
              <el-input v-model="formBasic.SystemPwd" class="ipt" />
            </div>
          </el-form-item>
          <el-form-item label="实名认证" :label-width="formLabelWidth">
            <el-button type="danger" plain>重置认证</el-button>
            <div class="iptBox">
              <span>姓名:</span>
              <el-input v-model="formBasic.namePwd" class="ipt" />
            </div>
            <div class="iptBox">
              <span>身份证号:</span>
              <el-input v-model="formBasic.Idname" class="ipt" />
            </div>
          </el-form-item>
          <el-form-item label="青少年密码" :label-width="formLabelWidth">
            <el-button type="danger" plain>重置密码</el-button>
            <div class="iptBox">
              <span>系统密码:</span>
              <el-input v-model="formBasic.shaonianPwd1" class="ipt" />
            </div>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button
            type="primary"
            @click="dialogFormVisible = false"
          >确 定</el-button>
          <el-button @click="dialogFormVisible = false">取 消</el-button>
        </div>
      </el-dialog>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 注册渠道信息
      UserInfo: {
        valuetime: [
          new Date(2000, 10, 10, 10, 10),
          new Date(2000, 10, 11, 10, 10)
        ],
        nickName: '',
        userId: '',
        phone: '',
        reg: '',
        platform: '',
        ID: ''
      },
      pickerOptions: {
        shortcuts: [
          {
            text: '最近一周',
            onClick(picker) {
              const end = new Date()
              const start = new Date()
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
              picker.$emit('pick', [start, end])
            }
          },
          {
            text: '最近一个月',
            onClick(picker) {
              const end = new Date()
              const start = new Date()
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
              picker.$emit('pick', [start, end])
            }
          },
          {
            text: '最近三个月',
            onClick(picker) {
              const end = new Date()
              const start = new Date()
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
              picker.$emit('pick', [start, end])
            }
          }
        ]
      },
      // 表格里面的数据
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
          zip: 200333
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1517 弄',
          zip: 200333
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1519 弄',
          zip: 200333
        },
        {
          date: '2016-05-03',
          name: '王小虎',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1516 弄',
          zip: 200333
        }
      ],
      // 模态框数据
      dialogFormVisible: false,
      formBasic: {
        SystemPwd: '', // 系统密码
        namePwd: '', // 姓名
        Idname: '', // 身份证号
        shaonianPwd1: '' // 青少年密码
      },
      formLabelWidth: '120px'
    }
    // 分页数据
  },
  methods: {
    // 分类的数据
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    },
    opendialong() {
      this.dialogFormVisible = true
    }
  }
}
</script>

<style scoped lang="scss">
.iptBox {
  display: flex;
  margin: 10px 0;
}
.iptBox span {
  display: inline-block;
  width: 80px;
  height: 20px;
  text-align: left;
}
.iptBox .ipt {
  width: 200px;
}
</style>

