<template>
  <div>
    <el-card class="box-card">
      <!-- 头部查询 -->
      <div class="headnav">
        <el-form :inline="true" :model="ExamibeData" class="demo-form-inline">
          <el-form-item>
            <el-date-picker
              v-model="ExamibeData.time"
              type="datetimerange"
              :picker-options="pickerOptions"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              align="right"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="ExamibeData.userId"
              placeholder="用户ID/手机号"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="ExamibeData.GuildId"
              placeholder="公会ID"
            />
          </el-form-item>
          <el-form-item>
            <el-select v-model="ExamibeData.TopClass" placeholder="顶级分类">
              <el-option value="游戏" />
              <el-option value="娱乐" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-select v-model="ExamibeData.SkillClass" placeholder="技能分类">
              <el-option value="王者荣耀" />
              <el-option value="和平精英" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-select v-model="ExamibeData.stale" placeholder="处理状况">
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
        <el-select v-model="ExamibeData.select">
          <el-option
            v-for="item in ExamibeData.options"
            :key="item.value"
            :value="item.value"
            :label="item.label"
          />
        </el-select>
      </div>
      <!-- 表格 -->
      <el-table :data="tableData" border style="width: 100%" class="tab">
        <el-table-column
          fixed
          prop="Ranking"
          label="申请时间"
          width="250"
          align="center"
        />
        <el-table-column prop="SkId" label="用户ID" width="120" align="center" />
        <el-table-column
          prop="Skname"
          label="用户昵称"
          width="120"
          align="center"
        />
        <el-table-column
          prop="proIcon"
          label="所属公会"
          width="120"
          align="center"
        />
        <el-table-column
          prop="TopClass"
          label="顶级分类"
          width="120"
          align="center"
        />
        <el-table-column
          prop="enStatus"
          label="技能分类"
          width="120"
          align="center"
        />
        <el-table-column
          prop="priceSmall"
          label="大神头像"
          width="120"
          align="center"
        />
        <el-table-column
          prop="priceMideen"
          label="服务类别"
          width="120"
          align="center"
        >
          <template>
            <el-button type="primary">查看</el-button>
          </template>
        </el-table-column>
        <el-table-column
          prop="priceheight"
          label="个人介绍"
          width="120"
          align="center"
        >
          <template>
            <el-button
              type="primary"
              class="btn"
              @click="TextDialog = true"
            >文字</el-button>
            <el-button
              type="primary"
              class="btn"
              @click="pictureDialog = true"
            >图片</el-button>
            <el-button
              type="primary"
              class="btn"
              @click="musicDialog = true"
            >语音</el-button>
          </template>
        </el-table-column>
        <el-table-column
          prop="AddTime"
          label="处理时间"
          width="200"
          align="center"
        />
        <el-table-column
          prop="updateTime"
          label="处理状况"
          width="120"
          align="center"
        />
        <el-table-column fixed="right" label="操作" width="150" align="center">
          <template>
            <el-button type="primary" class="btn">通过</el-button>
            <el-button type="danger" class="btn">拒绝</el-button>
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
      <!-- 文字模态框 -->
      <el-dialog
        title="文字"
        :visible.sync="TextDialog"
        center
        width="35%"
        class="dialog"
      >
        <el-input v-model="Text" type="textarea" />
        <div slot="footer" class="dialog-footer">
          <el-button
            class="sucBtn"
            type="success"
            plain
            @click="TextDialog = false"
          >完成</el-button>
        </div>
      </el-dialog>
      <!-- 图片模态框 -->
      <el-dialog
        title="图片"
        :visible.sync="pictureDialog"
        center
        width="35%"
        class="dialog"
      >
        <div class="imgbox">
          <img src="../../assets/401_images/401.gif" alt="" class="img">
        </div>

        <div slot="footer" class="dialog-footer">
          <el-button
            class="sucBtn"
            type="success"
            plain
            @click="pictureDialog = false"
          >完成</el-button>
        </div>
      </el-dialog>
      <!-- 音频模态框 -->
      <el-dialog
        title="语音"
        :visible.sync="musicDialog"
        center
        width="35%"
        class="dialog"
      >
        <div class="imgbox">
          <audio src="" controls />
        </div>

        <div slot="footer" class="dialog-footer">
          <el-button
            class="sucBtn"
            type="success"
            plain
            @click="musicDialog = false"
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
      ExamibeData: {
        SkillId: '',
        GuildId: '',
        TopClass: '',
        stale: '',
        sort: '',
        time: [new Date(2020, 8, 10, 10, 10), new Date(2020, 10, 11, 10, 10)],
        select: '最近申请', // 默认选中
        options: [
          {
            value: '最近申请',
            label: '最近申请'
          },
          {
            value: '最早申请',
            label: '最早申请'
          }
        ]
      },

      // 表格数据
      tableData: [
        {
          userId: 99,
          SkId: 110,
          Skname: '王者荣耀',
          proIcon: '',
          TopClass: '游戏',
          enStatus: '开启',
          priceSmall: '技能1:50局',
          priceMideen: '技能1:50局',
          priceheight: '技能1:50局',
          AddTime: '2020-10-09-10:45:32',
          updateTime: '2020-10-09-10:45:32'
        },
        {
          Ranking: 99,
          SkId: 110,
          Skname: '王者荣耀',
          proIcon: '',
          TopClass: '游戏',
          enStatus: '开启',
          priceSmall: '技能1:50局',
          priceMideen: '技能1:50局',
          priceheight: '技能1:50局',
          AddTime: '2020-10-09-10:45:32',
          updateTime: '2020-10-09-10:45:32'
        },
        {
          Ranking: 99,
          SkId: 110,
          Skname: '王者荣耀',
          proIcon: '',
          TopClass: '游戏',
          enStatus: '开启',
          priceSmall: '技能1:50局',
          priceMideen: '技能1:50局',
          priceheight: '技能1:50局',
          AddTime: '2020-10-09-10:45:32',
          updateTime: '2020-10-09-10:45:32'
        }
      ],
      // 时间选择
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
      // 文字
      TextDialog: false,
      Text: '',
      // 图片
      pictureDialog: false,
      // 音频
      musicDialog: false
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
.imgbox {
  text-align: center;
  .img {
    width: 200px;
    height: 200px;
  }
}
</style>
