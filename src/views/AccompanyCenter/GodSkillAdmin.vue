<template>
  <div>
    <el-card class="box-card">
      <!-- 头部查询 -->
      <div class="headnav">
        <el-form :inline="true" :model="GodSkillData" class="demo-form-inline">
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
            <el-select v-model="GodSkillData.TopClass" placeholder="顶级分类">
              <el-option value="游戏" />
              <el-option value="娱乐" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-select v-model="GodSkillData.SkillClass" placeholder="技能分类">
              <el-option value="王者荣耀" />
              <el-option value="和平精英" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-select v-model="GodSkillData.stale" placeholder="处理状况">
              <el-option value="待处理" />
              <el-option value="已通过" />
              <el-option value="已拒绝" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">查找</el-button>
          </el-form-item>
          <el-form-item>
            <el-button type="danger">导出数据</el-button>
          </el-form-item>
        </el-form>
        <el-select v-model="GodSkillData.sort">
          <el-option value="最近开通" />
          <el-option value="最早开通" />
        </el-select>
      </div>
      <!-- 表格 -->
      <el-table :data="SKillTableData" border style="width: 100%" class="tab">
        <el-table-column
          fixed
          prop="OpenTime"
          label="开通时间"
          width="250"
          align="center"
        />
        <el-table-column
          prop="TopClass"
          label="顶级分类"
          width="120"
          align="center"
        />
        <el-table-column
          prop="SkillClass"
          label="技能分类"
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
          width="120"
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
          prop="SkillLevel"
          label="技能等级"
          width="120"
          align="center"
        />
        <el-table-column prop="Price" label="价格" width="120" align="center" />
        <el-table-column
          prop="OrderTime"
          label="接单时间"
          width="200"
          align="center"
        />
        <el-table-column
          prop="RecOrders"
          label="接单"
          width="120"
          align="center"
        >
          <template>
            <el-button type="primary">开启</el-button>
          </template>
        </el-table-column>
        <el-table-column
          prop="DisOrders"
          label="派单"
          width="120"
          align="center"
        >
          <template>
            <el-button type="danger">关闭</el-button>
          </template>
        </el-table-column>
        <el-table-column
          prop="ServiceTime"
          label="服务次数"
          width="120"
          align="center"
        />
        <el-table-column
          prop="CurrentState"
          label="当前状态"
          width="120"
          align="center"
        />
        <el-table-column fixed="right" label="操作" width="150" align="center">
          <template>
            <el-button type="primary" class="btn">刷新资料</el-button>
            <el-button
              type="danger"
              class="btn"
              @click="dialogFormVisible = true"
            >编辑价格</el-button>
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
    <!-- 编辑价格模态框 -->
    <el-dialog
      title="编辑技能价格"
      :visible.sync="dialogFormVisible"
      center
      width="30%"
      class="dialog"
    >
      <el-form :model="formData">
        <el-form-item label="服务1" :label-width="formLabelWidth">
          {{ formData.ServiceOne }}
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData.PriPrice"
            placeholder="自定义初级价格(GO币)"
          />
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData.MediatePrice"
            placeholder="自定义中级价格(GO币)"
          />
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData.SeniorPrice"
            placeholder="自定义高级价格(GO币)"
          />
        </el-form-item>
      </el-form>
      <el-form :model="formData2">
        <el-form-item label="服务2" :label-width="formLabelWidth">
          {{ formData.ServiceOne }}
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData2.PriPrice"
            placeholder="自定义初级价格(GO币)"
          />
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData2.MediatePrice"
            placeholder="自定义中级价格(GO币)"
          />
        </el-form-item>
        <el-form-item :label-width="formLabelWidth">
          <el-input
            v-model="formData2.SeniorPrice"
            placeholder="自定义高级价格(GO币)"
          />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button
          class="sucessBtn"
          type="success"
          plain
          @click="dialogFormVisible = false"
        >完成</el-button>
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
        sort: '最近开通'
      },
      // 表格数据
      SKillTableData: [
        {
          OpenTime: '2020-10-09-10:45:32',
          TopClass: '游戏',
          SkillClass: '王者荣耀',
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SkillLevel: '初级',
          Price: '技能1:50局',
          OrderTime: '2020-10-09-10:45:32',
          ServiceTime: 12,
          CurrentState: '接单中'
        },
        {
          OpenTime: '2020-10-09-10:45:32',
          TopClass: '游戏',
          SkillClass: '王者荣耀',
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SkillLevel: '初级',
          Price: '技能1:50局',
          OrderTime: '2020-10-09-10:45:32',
          ServiceTime: 12,
          CurrentState: '接单中'
        },
        {
          OpenTime: '2020-10-09-10:45:32',
          TopClass: '游戏',
          SkillClass: '王者荣耀',
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SkillLevel: '初级',
          Price: '技能1:50局',
          OrderTime: '2020-10-09-10:45:32',
          ServiceTime: 12,
          CurrentState: '接单中'
        },
        {
          OpenTime: '2020-10-09-10:45:32',
          TopClass: '游戏',
          SkillClass: '王者荣耀',
          GodId: 232323,
          GodNickname: '张三丰',
          GodPhone: 13989898787,
          GodHeader: '',
          Guild: '王者公会',
          SkillLevel: '初级',
          Price: '技能1:50局',
          OrderTime: '2020-10-09-10:45:32',
          ServiceTime: 12,
          CurrentState: '接单中'
        }
      ],
      // 模态框数据
      dialogFormVisible: false,
      formData: {
        ServiceOne: '局/30分钟/15分钟',
        PriPrice: '',
        MediatePrice: '',
        SeniorPrice: ''
      },
      formData2: {
        ServiceOne: '天/720分钟/360分钟',
        PriPrice: '',
        MediatePrice: '',
        SeniorPrice: ''
      },
      formLabelWidth: '180px'
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
    width: 200px;
  }
}
.sucessBtn {
  width: 150px;
  height: 36px;
  text-align: center;
}
</style>
