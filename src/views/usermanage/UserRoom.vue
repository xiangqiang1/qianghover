<template>
  <div>
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <el-form :inline="true" :model="roomData" class="demo-form-inline">
          <el-form-item label="昵称:">
            <el-input
              v-model="roomData.nickName"
              placeholder="请输入昵称"
            />
          </el-form-item>
          <el-form-item label="用户ID:">
            <el-input
              v-model="roomData.userId"
              placeholder="请输入ID"
            />
          </el-form-item>
          <el-form-item label="手机号:">
            <el-input
              v-model="roomData.phone"
              placeholder="请输入手机号"
            />
          </el-form-item>
          <el-form-item label="房间号:">
            <el-input
              v-model="roomData.roomNum"
              placeholder="请输入房间号"
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
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column fixed prop="date" label="昵称" width="150" />
        <el-table-column prop="name" label="用户ID" width="120" />
        <el-table-column prop="province" label="手机号" width="120" />
        <el-table-column prop="city" label="房间号" width="120" />
        <el-table-column prop="address" label="房间名字" width="300" />
        <el-table-column prop="zip" label="房间总流水" width="120" />
        <el-table-column prop="zip" label="房间礼物数" width="120" />
        <el-table-column prop="zip" label="最近上播时间" width="200" />
        <el-table-column prop="zip" label="最近下播时间" width="200" />
        <el-table-column fixed="right" label="修改房间" align="center">
          <template>
            <el-button
              type="primary"
              size="small"
              @click="dialogFormVisible = true"
            >编辑</el-button>
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
    <!-- 编辑模态框 -->
    <el-dialog
      title="编辑页面"
      :visible.sync="dialogFormVisible"
      center
      width="30%"
    >
      <div class="dialogMain">
        <el-form :model="formRoom">
          <el-form-item label="房间名:" :label-width="formLabelWidth">
            <el-input v-model="formRoom.name" autocomplete="off" />
          </el-form-item>
          <el-form-item label="话题设置:" :label-width="formLabelWidth">
            <el-input v-model="formRoom.setting" type="textarea" />
          </el-form-item>
          <el-form-item label="房间标签:" :label-width="formLabelWidth">
            <el-radio
              v-for="item in formRoom.radioList"
              :key="item"
              v-model="formRoom.radio"
              :label="item"
              @change="changeParty"
            >{{ item }}</el-radio>
            <!-- 派对的选项 -->
            <div v-show="isShow">
              <el-checkbox
                v-model="checkAll"
                :indeterminate="isIndeterminate"
                @change="handleCheckAllChange"
              >全选</el-checkbox>
              <el-checkbox-group
                v-model="checkedCities"
                @change="handleCheckedCitiesChange"
              >
                <el-checkbox v-for="city in cities" :key="city" :label="city">{{
                  city
                }}</el-checkbox>
              </el-checkbox-group>
            </div>
          </el-form-item>
          <el-form-item label="玩法推荐:" :label-width="formLabelWidth">
            <el-input v-model="formRoom.playing" type="textarea" />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button
            type="primary"
            @click="dialogFormVisible = false"
          >确 定</el-button>
          <el-button @click="dialogFormVisible = false">取 消</el-button>
        </div>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 头部房间信息
      roomData: {
        nickName: '',
        userId: '',
        phone: '',
        roomNum: ''
      },
      // 表格
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
      formLabelWidth: '100px', // 模态框小标题的宽度
      dialogFormVisible: false,
      // 模态框里面的动态数据
      formRoom: {
        name: '',
        setting: '',
        playing: '',
        radio: '1', // 房间标签单选框
        radioList: ['派对', '电台']
      },
      // 模态框派对的选项
      isShow: false, // 是否显示派对子标签的标杆
      checkAll: false,
      checkedCities: [],
      cities: [], // 循环的数组
      isIndeterminate: true
    }
  },
  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    },
    // 监听派对的变化
    handleCheckAllChange(val) {
      this.checkedCities = val ? this.cities : []
      this.isIndeterminate = false
    },
    handleCheckedCitiesChange(value) {
      const checkedCount = value.length
      this.checkAll = checkedCount === this.cities.length
      this.isIndeterminate =
        checkedCount > 0 && checkedCount < this.cities.length
    },
    // 监听是否显示派对子菜单
    changeParty(res) {
      if (res == '派对') {
        this.cities = ['派单', '相亲交友', '女神', '男神', '点歌', '娱乐']
        this.isShow = true
      } else if (res == '电台') {
        this.isShow = true
        this.cities = ['脱口秀', '唱歌', '萌新']
      }
    }
  }
}
</script>

<style scoped lang='scss'>
.dialogMain {
  width: 500px;
  height: 460px;
  overflow: auto;
  padding-right: 15px;
  .dialog-footer {
    margin-top: 30px;
    text-align: center;
  }
}
</style>
