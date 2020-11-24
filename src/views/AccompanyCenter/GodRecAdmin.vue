<template>
  <div>
    <el-card class="box-card">
      <!-- 头部查询 -->
      <div class="headnav">
        <el-form :inline="true" :model="GodSkillData" class="demo-form-inline">
          <el-form-item>
            <el-button
              type="success"
              @click="dialogFormVisible = true"
            >新增推荐</el-button>
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="GodSkillData.number"
              placeholder="大神ID/手机号"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="GodSkillData.Guildname"
              placeholder="大神昵称"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="GodSkillData.Guildname"
              placeholder="公会ID"
            />
          </el-form-item>
          <el-form-item>
            <el-select v-model="GodSkillData.SkillClass" placeholder="推荐位置">
              <el-option value="王者荣耀" />
              <el-option value="和平精英" />
              <el-option value="吃鸡" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">查找</el-button>
          </el-form-item>
        </el-form>
        <el-select v-model="GodSkillData.sort">
          <el-option value="最近推荐" />
          <el-option value="最早推荐" />
        </el-select>
      </div>
      <!-- 表格 -->
      <el-table :data="SKillTableData" border style="width: 100%" class="tab">
        <el-table-column
          fixed
          prop="RecTime"
          label="推荐时间"
          width="250"
          align="center"
        />
        <el-table-column
          prop="RecPosition"
          label="推荐位置"
          width="250"
          align="center"
        />
        <el-table-column
          prop="Ranking"
          label="排序权重"
          width="120"
          align="center"
        />
        <el-table-column prop="GodId" label="大神ID" width="120" align="center" />
        <el-table-column
          prop="GodNickname"
          label="大神昵称"
          width="120"
          align="center"
        />
        <el-table-column
          prop="GodPhone"
          label="手机号"
          width="120"
          align="center"
        />
        <el-table-column
          prop="GodHeader"
          label="大神头像"
          width="125"
          align="center"
        >
          <template>
            <img src="" alt="">
          </template>
        </el-table-column>
        <el-table-column
          prop="Guild"
          label="所属公会"
          width="120"
          align="center"
        />
        <el-table-column
          prop="SurplusRecTime"
          label="剩余推荐时间"
          width="200"
          align="center"
        />
        <el-table-column fixed="right" label="操作" width="150" align="center">
          <template>
            <el-button
              type="primary"
              class="btn"
              @click="EditWeight = true"
            >编辑权重</el-button>
            <el-button type="danger" class="btn">删除</el-button>
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
    <!-- 新增推荐的模态框 -->
    <el-dialog
      title="新增推荐"
      :visible.sync="dialogFormVisible"
      center
      width="35%"
      class="dialog"
    >
      <el-form :model="GodformData">
        <el-form-item label="推荐位置" :label-width="formLabelWidth">
          <el-select v-model="GodformData.address">
            <el-option
              v-for="item in GodformData.option1"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </el-form-item>
        <el-form-item label="推荐时间" :label-width="formLabelWidth">
          <el-select v-model="GodformData.Rectime">
            <el-option
              v-for="item in GodformData.option2"
              :key="item.label"
              :label="item.label"
              :value="item.value"
            />
          </el-select>
        </el-form-item>
        <el-form-item label="推荐大神" :label-width="formLabelWidth">
          <el-input
            v-model="GodformData.RecGod"
            autocomplete="off"
            placeholder="请输入用户ID"
          />
        </el-form-item>
        <el-form-item label="设置权重" :label-width="formLabelWidth">
          <el-input
            v-model="GodformData.weight"
            autocomplete="off"
            placeholder="请输入权重值"
          />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button
          class="sucBtn"
          type="success"
          plain
          @click="dialogFormVisible = false"
        >确认</el-button>
      </div>
    </el-dialog>
    <!-- 编辑权重的模态框 -->
    <el-dialog
      title="编辑权重"
      :visible.sync="EditWeight"
      center
      width="35%"
      class="dialog"
    >
      <el-form :model="EditWeightData">
        <el-form-item label="设置权重" :label-width="formLabelWidth">
          <el-input v-model="EditWeightData.name" placeholder="请编辑权重值" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button
          class="sucBtn"
          type="success"
          plain
          @click="EditWeight = false"
        >确 认</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 头部搜索数据
      GodSkillData: {
        number: '',
        Guildname: '',
        TopClass: '',
        stale: '',
        sort: '最近推荐'
      },
      // 表格数据
      SKillTableData: [
        {
          RecTime: '2020-10-09-10:45:32',
          RecPosition: '大神列表页-和平精英',
          Ranking: 99,
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SurplusRecTime: '33分钟23秒'
        },
        {
          RecTime: '2020-10-09-10:45:32',
          RecPosition: '大神列表页-和平精英',
          Ranking: 99,
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SurplusRecTime: '33分钟23秒'
        },
        {
          RecTime: '2020-10-09-10:45:32',
          RecPosition: '大神列表页-和平精英',
          Ranking: 99,
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SurplusRecTime: '33分钟23秒'
        },
        {
          RecTime: '2020-10-09-10:45:32',
          RecPosition: '大神列表页-和平精英',
          Ranking: 99,
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SurplusRecTime: '33分钟23秒'
        }
      ],
      //   新增编辑模态框
      dialogFormVisible: false,
      GodformData: {
        address: '大神列表页-新人', // 推荐位置
        Rectime: '12小时', // 推荐时间
        RecGod: '', // ID
        weight: '', // 权重
        option1: [
          { label: '大神列表页-和平精英', value: '大神列表页-和平精英' },
          { label: '大神列表页-王者荣耀', value: '大神列表页-王者荣耀' },
          { label: '大神列表页-新人', value: '大神列表页-新人' }
        ],
        option2: [
          { label: '12小时', value: '12小时' },
          { label: '24小时', value: '24小时' },
          { label: '36小时', value: '36小时' },
          { label: '72小时', value: '72小时' }
        ]
      },
      formLabelWidth: '200px',
      // 编辑权重
      EditWeight: false,
      EditWeightData: {
        name: ''
      }
    }
  },

  methods: {
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
.headnav {
  display: flex;
  justify-content: space-between;
}
.btn {
  margin: 5px 0;
}
.dialog {
  .el-input {
    width: 217px;
  }
}
.sucBtn {
  width: 150px;
  height: 36px;
  text-align: center;
}
</style>
