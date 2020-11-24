<template>
  <div>
    <el-card class="box-card">
      <!-- 头部查询 -->
      <div class="headnav">
        <el-form :inline="true" :model="formData" class="demo-form-inline">
          <el-form-item>
            <el-button
              type="success"
              @click="NewFielddialog = true"
            >新增字段</el-button>
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="formData.SkillId"
              placeholder="字段ID"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="formData.Skillname"
              placeholder="字段名"
            />
          </el-form-item>
          <el-form-item>
            <el-button type="primary">查找</el-button>
          </el-form-item>
        </el-form>

        <div class="right">
          <el-select v-model="formData.sort">
            <el-option value="按排序权重降序" />
            <el-option value="按排序权重升序" />
          </el-select>
          <el-button type="warning" @click="black">返回列表</el-button>
        </div>
      </div>
      <!-- 标签页的选项卡 -->
      <el-tabs v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="可接段位" name="first">
          <el-table :data="tableData" stripe style="width: 100%" border>
            <el-table-column prop="date" label="排序权重" align="center" />
            <el-table-column prop="name" label="字段ID" align="center" />
            <el-table-column prop="address" label="字段名" align="center" />
            <el-table-column prop="address" label="操作" align="center">
              <template>
                <el-button
                  type="primary"
                  @click="NewEditDialog = true"
                >编辑</el-button>
                <el-button type="danger">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-tab-pane>
        <el-tab-pane label="可接专区" name="second">可接专区</el-tab-pane>
        <el-tab-pane label="擅长英雄" name="third">擅长英雄</el-tab-pane>
      </el-tabs>
      <!-- 新增字段的模态框 -->
      <el-dialog
        title="新增推荐"
        :visible.sync="NewFielddialog"
        center
        width="35%"
        class="dialog"
      >
        <el-form :model="KingsData">
          <el-form-item label="技能分类" :label-width="formLabelWidth">
            <el-select v-model="KingsData.class">
              <el-option
                v-for="item in KingsData.option1"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="排序权重" :label-width="formLabelWidth">
            <el-input
              v-model="KingsData.sort"
              placeholder="请输入排序权重"
            />
          </el-form-item>
          <el-form-item label="字段名称" :label-width="formLabelWidth">
            <el-input
              v-model="KingsData.name"
              autocomplete="off"
              placeholder="请输入字段名称"
            />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button
            class="sucBtn"
            type="success"
            plain
            @click="NewFielddialog = false"
          >完成</el-button>
        </div>
      </el-dialog>
      <!-- 编辑字段的模态框 -->
      <el-dialog
        title="编辑字段"
        :visible.sync="NewEditDialog"
        center
        width="35%"
        class="dialog"
      >
        <el-form :model="editData">
          <el-form-item label="排序权重" :label-width="formLabelWidth">
            <el-input
              v-model="editData.sort"
              placeholder="请输入排序权重"
            />
          </el-form-item>
          <el-form-item label="字段名称" :label-width="formLabelWidth">
            <el-input
              v-model="editData.name"
              autocomplete="off"
              placeholder="请输入字段名称"
            />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button
            class="sucBtn"
            type="success"
            plain
            @click="NewEditDialog = false"
          >完成</el-button>
        </div>
      </el-dialog>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 头部搜索数据
      formData: {
        SkillId: '',
        Skillname: '',
        TopClass: '',
        stale: '',
        sort: '按排序权重降序'
      },
      activeName: 'first', // 标签页选项卡的激活
      // 表格数据
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
      // 新增字段的模态框数据
      KingsData: {
        class: '',
        sort: '',
        name: '',
        option1: ['青铜', '黄金']
      },
      formLabelWidth: '210px',
      NewFielddialog: false, // 新增字段
      // 编辑字段的模态框数据
      NewEditDialog: false,
      editData: {
        sort: '',
        name: ''
      }
    }
  },
  methods: {
    black() {
      this.$router.push('/AccompanyCenter/SkillClassAdmin')
    },
    handleClick(tab, event) {
      console.log(tab, event)
    }
  }
}
</script>

<style lang="scss" scoped>
.headnav {
  display: flex;
  justify-content: space-between;
  .right {
    .el-button {
      margin-left: 20px;
    }
  }
}
.dialog {
  .el-input {
    width: 217px;
  }
}
</style>
