<template>
  <div>
    <el-card class="box-card">
      <!-- 头部查询 -->
      <div class="headnav">
        <el-form :inline="true" :model="formData" class="demo-form-inline">
          <el-form-item>
            <el-button
              type="success"
              @click="dialogFormVisible1 = true"
            >新增技能</el-button>
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="formData.SkillId"
              placeholder="技能ID"
            />
          </el-form-item>
          <el-form-item>
            <el-input
              v-model="formData.Skillname"
              placeholder="技能名"
            />
          </el-form-item>
          <el-form-item>
            <el-select v-model="formData.TopClass" placeholder="顶级分类">
              <el-option value="游戏" />
              <el-option value="娱乐" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-select v-model="formData.stale" placeholder="启用状态">
              <el-option value="开启" />
              <el-option value="关闭" />
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">查找</el-button>
          </el-form-item>
        </el-form>
        <el-select v-model="formData.sort">
          <el-option value="按排序权重降序" />
          <el-option value="按排序权重升序" />
        </el-select>
      </div>
      <!-- 表格 -->
      <el-table :data="tableData" border style="width: 100%" class="tab">
        <el-table-column
          fixed
          prop="Ranking"
          label="排序权重"
          width="150"
          align="center"
        />
        <el-table-column prop="SkId" label="技能ID" width="120" align="center" />
        <el-table-column
          prop="Skname"
          label="技能名称"
          width="120"
          align="center"
        />
        <el-table-column
          prop="proIcon"
          label="产品图标"
          width="120"
          align="center"
        >
          <template>
            <img src="" alt="">
          </template>
        </el-table-column>
        <el-table-column
          prop="TopClass"
          label="顶级分类"
          width="120"
          align="center"
        />
        <el-table-column
          prop="enStatus"
          label="启用状态"
          width="120"
          align="center"
        />
        <el-table-column
          prop="priceSmall"
          label="初级价格"
          width="120"
          align="center"
        />
        <el-table-column
          prop="priceMideen"
          label="中级价格"
          width="120"
          align="center"
        />
        <el-table-column
          prop="priceheight"
          label="高级价格"
          width="120"
          align="center"
        />
        <el-table-column
          prop="AddTime"
          label="添加时间"
          width="200"
          align="center"
        />
        <el-table-column
          prop="updateTime"
          label="更新时间"
          width="200"
          align="center"
        />
        <el-table-column
          prop="tese"
          label="特色字段配置"
          width="120"
          align="center"
        >
          <template>
            <el-button type="primary" @click="editing">字段编辑</el-button>
          </template>
        </el-table-column>
        <el-table-column fixed="right" label="操作" width="150" align="center">
          <template>
            <el-button
              type="primary"
              class="btn"
              @click="basicData = true"
            >资料编辑</el-button>
            <el-button
              type="primary"
              class="btn"
              @click="EditingSkill = true"
            >价格编辑</el-button>
            <el-button type="danger" class="btn">关闭</el-button>
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
      <!-- 新增技能的模态框1 -->
      <el-dialog
        title="新增技能"
        :visible.sync="dialogFormVisible1"
        center
        width="30%"
        class="dialogBox"
      >
        <!-- 模态框中间内容 -->
        <div class="dialogMain">
          <!-- 基础资料 -->
          <el-form :model="formdialogData1" class="formData">
            <el-form-item label="顶级分类:" :label-width="formLabelWidth">
              <el-select v-model="formdialogData1.TopClass">
                <el-option
                  v-for="item in formdialogData1.options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
            <el-form-item label="排序权重:" :label-width="formLabelWidth">
              <el-input
                v-model="formdialogData1.Ranking"
                placeholder="请按顺序输入权重"
              />
            </el-form-item>
            <el-form-item label="产品名称:" :label-width="formLabelWidth">
              <el-input
                v-model="formdialogData1.ProductName"
                placeholder="请按顺序输入权重"
              />
            </el-form-item>
            <el-form-item label="产品图标:" :label-width="formLabelWidth">
              <el-upload
                class="avatar-uploader"
                action="https://jsonplaceholder.typicode.com/posts/"
                :show-file-list="false"
                :on-success="handleAvatarSuccess"
              >
                <img
                  v-if="formdialogData1.imageUrl"
                  :src="formdialogData1.imageUrl"
                  class="avatar"
                >
                <i v-else class="el-icon-plus avatar-uploader-icon" />
              </el-upload>
            </el-form-item>
            <el-form-item label="服务方式:" :label-width="formLabelWidth">
              <el-select v-model="formdialogData1.ServiceMode">
                <el-option
                  v-for="item in formdialogData1.optionService"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-form>
          <!-- 服务价格 -->
          <el-form :model="formdialogData2" class="formData">
            <el-form-item label="服务1" :label-width="formLabelWidth">
              <el-select
                v-model="formdialogData2.ServiceMode"
                placeholder="陪玩方式"
                @change="PlayWithChange"
              >
                <el-option
                  v-for="item in formdialogData2.PlayWith"
                  :key="item"
                  :value="item"
                />
              </el-select>
            </el-form-item>
            <el-form-item :label-width="formLabelWidth">
              <el-select
                v-model="formdialogData2.time"
                placeholder="陪玩时长"
                :disabled="formdialogData2.isDisabled"
              >
                <el-option
                  v-for="item in formdialogData2.optionsTime"
                  :key="item"
                  :value="item"
                />
              </el-select>
            </el-form-item>
            <el-form-item :label-width="formLabelWidth">
              <el-select
                v-model="formdialogData2.proTime"
                placeholder="保护时间"
                :disabled="formdialogData2.isDisabled"
              >
                <el-option
                  v-for="item in formdialogData2.optionsProTime"
                  :key="item"
                  :value="item"
                />
              </el-select>
            </el-form-item>
            <el-form-item :label-width="formLabelWidth">
              <el-input
                v-model="formdialogData2.smallPirce"
                placeholder="请输入初级价格(Go币)"
              />
            </el-form-item>
            <el-form-item :label-width="formLabelWidth">
              <el-input
                v-model="formdialogData2.middPirce"
                placeholder="请输入中级价格(Go币)"
                disabled
              />
            </el-form-item>
            <el-form-item :label-width="formLabelWidth">
              <el-input
                v-model="formdialogData2.HeigthPirce"
                placeholder="请输入高级价格(Go币)"
                disabled
              />
            </el-form-item>
          </el-form>
          <!-- 特色字段 -->
          <div class="Feature">
            <!-- 上方说明 -->
            <div class="titleText">
              <div class="teshe">特色字段</div>
              <div>
                具体字段如何添加:请完成技能添加后,点击特色字段配置的[编辑]按钮进行添加请慎重选择,后台不可更改
              </div>
            </div>
            <!-- 游戏类 -->
            <div v-if="this.formdialogData1.TopClass == '游戏'" class="game">
              <h3>游戏类</h3>
              <div class="switchList">
                <div v-for="item in SwList" :key="item.name" class="swItem">
                  <span>{{ item.name }}</span>
                  <el-switch
                    v-model="item.value"
                    active-color="#13ce66"
                    inactive-color="#ff4949"
                    :active-value="item.label"
                    @change="switchChange"
                  />
                </div>
              </div>
            </div>
            <!-- 娱乐 -->
            <div v-if="this.formdialogData1.TopClass == '娱乐'" class="game">
              <h3>娱乐类</h3>
              <div class="switchList">
                <div v-for="item in TsLisst" :key="item.label" class="swItem">
                  <span>{{ item.name }}</span>
                  <el-switch
                    v-model="item.value"
                    active-color="#13ce66"
                    inactive-color="#ff4949"
                    :active-value="item.label"
                    @change="switchChange"
                  />
                </div>
              </div>
            </div>
          </div>
          <!-- 审核字段 -->
          <div class="Audit">
            <!-- 上方说明 -->
            <div class="titleText">
              <div class="teshe">审核字段</div>
              <div>选中字段将在大神提交技能必填(单选)</div>
              <div>请慎重选择,后台不可更改</div>
            </div>
            <!-- 单选框 -->
            <div class="radio">
              <el-radio-group v-model="Radio">
                <el-radio v-for="item in RadioList" :key="item" :label="item">{{
                  item
                }}</el-radio>
              </el-radio-group>
            </div>
          </div>
        </div>
        <div slot="footer" class="dialog-footer">
          <el-button type="success" @click="AddComplete">确定新增</el-button>
        </div>
      </el-dialog>
      <!-- 基础资料编辑 -->
      <el-dialog
        title="编辑基础资料"
        :visible.sync="basicData"
        center
        width="30%"
        class="dialogBox"
      >
        <el-form :model="formbasicData" class="formData">
          <el-form-item label="顶级分类:" :label-width="formLabelWidth">
            <el-select v-model="formbasicData.TopClass">
              <el-option
                v-for="item in formbasicData.options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </el-form-item>
          <el-form-item label="排序权重:" :label-width="formLabelWidth">
            <el-input
              v-model="formbasicData.Ranking"
              placeholder="请按顺序输入权重"
            />
          </el-form-item>
          <el-form-item label="产品名称:" :label-width="formLabelWidth">
            <el-input
              v-model="formbasicData.ProductName"
              placeholder="请按顺序输入权重"
            />
          </el-form-item>
          <el-form-item label="产品图标:" :label-width="formLabelWidth">
            <el-upload
              class="avatar-uploader"
              action="https://jsonplaceholder.typicode.com/posts/"
              :show-file-list="false"
              :on-success="handleAvatarSuccess"
            >
              <img
                v-if="formbasicData.imageUrl"
                :src="formbasicData.imageUrl"
                class="avatar"
              >
              <i v-else class="el-icon-plus avatar-uploader-icon" />
            </el-upload>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="success" @click="basicData = false">完成</el-button>
        </div>
      </el-dialog>
      <!-- 编辑技能价格 -->
      <el-dialog
        title="编辑服务价格"
        :visible.sync="EditingSkill"
        center
        width="30%"
        class="dialogBox"
      >
        <!-- 选择服务方式 -->
        <el-select
          v-model="ServiceChange"
          placeholder="服务方式1"
          class="selectChange"
          @change="changeSer"
        >
          <el-option
            v-for="item in ServiceChange_data"
            :key="item"
            :value="item"
          />
        </el-select>
        <!-- 服务方式1 -->
        <el-form :model="EditingData1" class="formData">
          <el-form-item label="服务1" :label-width="formLabelWidth">
            <el-select
              v-model="EditingData1.ServiceMode"
              placeholder="陪玩方式"
              @change="PlayChange1"
            >
              <el-option
                v-for="item in EditingData1.PlayWith"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-select
              v-model="EditingData1.time"
              placeholder="陪玩时长"
              :disabled="EditingData1.isDisabled"
            >
              <el-option
                v-for="item in EditingData1.optionsTime"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-select
              v-model="EditingData1.proTime"
              placeholder="保护时间"
              :disabled="EditingData1.isDisabled"
            >
              <el-option
                v-for="item in EditingData1.optionsProTime"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData1.smallPirce"
              placeholder="请输入初级价格(Go币)"
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData1.middPirce"
              placeholder="请输入中级价格(Go币)"
              disabled
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData1.HeigthPirce"
              placeholder="请输入高级价格(Go币)"
              disabled
            />
          </el-form-item>
        </el-form>
        <!-- 服务方式2 -->
        <el-form v-show="isShow" :model="EditingData2" class="formData">
          <el-form-item label="服务2" :label-width="formLabelWidth">
            <el-select
              v-model="EditingData2.ServiceMode"
              placeholder="陪玩方式"
              @change="PlayChange2"
            >
              <el-option
                v-for="item in EditingData2.PlayWith"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-select
              v-model="EditingData2.time"
              placeholder="陪玩时长"
              :disabled="EditingData2.isDisabled"
            >
              <el-option
                v-for="item in EditingData2.optionsTime"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-select
              v-model="EditingData2.proTime"
              placeholder="保护时间"
              :disabled="EditingData2.isDisabled"
            >
              <el-option
                v-for="item in EditingData2.optionsProTime"
                :key="item"
                :value="item"
              />
            </el-select>
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData2.smallPirce"
              placeholder="请输入初级价格(Go币)"
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData2.middPirce"
              placeholder="请输入中级价格(Go币)"
              disabled
            />
          </el-form-item>
          <el-form-item :label-width="formLabelWidth">
            <el-input
              v-model="EditingData2.HeigthPirce"
              placeholder="请输入高级价格(Go币)"
              disabled
            />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button
            type="success"
            @click="EditingSkill = false"
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
      // 表格数据
      tableData: [
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
      formLabelWidth: '180px', // 模态框里面小标题的宽度
      dialogFormVisible1: false, // 模态框1
      dialogFormVisible2: false, // 模态框2
      dialogFormVisible3: false, // 模态框3
      dialogFormVisible4: false, // 模态框4
      basicData: false, // 编辑基础资料
      EditingSkill: false, // 编辑服务价格
      // 基础资料
      formdialogData1: {
        TopClass: '游戏',
        Ranking: '',
        ProductName: '',
        ServiceMode: '方式一',
        // 顶级分类
        options: [
          {
            label: '游戏',
            value: '游戏'
          },
          {
            label: '娱乐',
            value: '娱乐'
          }
        ],
        // 服务方式
        optionService: [
          {
            label: '方式一',
            value: '方式一'
          },
          {
            label: '方式二',
            value: '方式二'
          }
        ]
      },
      // 服务价格资料
      formdialogData2: {
        ServiceMode: '', // 陪玩方式
        time: '', // 陪玩时长
        proTime: '', // 保护时长
        isDisabled: true, // 是否禁用的标杆
        smallPirce: '', // 初级价格
        middPirce: '', // 中级价格
        HeigthPirce: '', // 高级价格
        optionsTime: [
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟',
          '40分钟',
          '50分钟'
        ],
        optionsProTime: [
          '5分钟',
          '7分钟',
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟'
        ],
        PlayWith: ['局', '次', '天', '半小时', '小时'],
        imageUrl: '' // 头像上传的路径
      },

      // 游戏类
      SwList: [
        { name: '可用大区', value: '', label: '可用大区' },
        { name: '可接段位', value: '', label: '可接段位' },
        { name: '擅长位置', value: '', label: '擅长位置' },
        { name: '擅长英雄', value: '', label: '擅长英雄' },
        { name: '游戏等级', value: '', label: '游戏等级' },
        { name: '擅长地图', value: '', label: '擅长地图' }
      ],
      // 娱乐类
      TsLisst: [{ name: '特色', value: '', label: '特色' }],
      // 审核字段的值
      Radio: '可接段位',
      // 审核字段的数组
      RadioList: ['可接段位', '游戏等级', '特色'],
      // 编辑基础资料
      formbasicData: {
        TopClass: '游戏',
        Ranking: '',
        ProductName: '',
        imageUrl: '' // 头像上传的路径
      },
      // 编辑技能的数据
      // 服务方式1
      EditingData1: {
        ServiceMode: '', // 陪玩方式
        time: '', // 陪玩时长
        proTime: '', // 保护时长
        isDisabled: true, // 是否禁用的标杆
        smallPirce: '', // 初级价格
        middPirce: '', // 中级价格
        HeigthPirce: '', // 高级价格
        PlayWith: ['局', '次', '天', '半小时', '小时'],
        optionsTime: [
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟',
          '40分钟',
          '50分钟'
        ],
        optionsProTime: [
          '5分钟',
          '7分钟',
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟'
        ]
      },
      // 服务方式2
      EditingData2: {
        ServiceMode: '', // 陪玩方式
        time: '', // 陪玩时长
        proTime: '', // 保护时长
        isDisabled: true, // 是否禁用的标杆
        smallPirce: '', // 初级价格
        middPirce: '', // 中级价格
        HeigthPirce: '', // 高级价格
        PlayWith: ['局', '次', '天', '半小时', '小时'],
        optionsTime: [
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟',
          '40分钟',
          '50分钟'
        ],
        optionsProTime: [
          '5分钟',
          '7分钟',
          '10分钟',
          '15分钟',
          '20分钟',
          '30分钟'
        ]
      },
      // 服务方式的切换
      ServiceChange: '一种服务方式',
      ServiceChange_data: ['一种服务方式', '二种服务方式'],
      isShow: false // 切换服务方式的标杆
    }
  },

  methods: {
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
    },
    // 监听头像上传成功的回调
    handleAvatarSuccess(res, file) {
      this.imageUrl = URL.createObjectURL(file.raw)
    },
    switchChange(res) {
      console.log(res)
    },
    // 新增技能监听陪玩方式的改变
    PlayWithChange(res) {
      res == '局' || res == '次'
        ? (this.formdialogData2.isDisabled = false)
        : (this.formdialogData2.isDisabled = true)
      if (res == '天') {
        this.formdialogData2.time = '720分钟'
        this.formdialogData2.proTime = '360分钟'
      } else if (res == '小时') {
        this.formdialogData2.time = '60分钟'
        this.formdialogData2.proTime = '30分钟'
      } else if (res == '半小时') {
        this.formdialogData2.time = '30分钟'
        this.formdialogData2.proTime = '15分钟'
      } else {
        this.formdialogData2.time = ''
        this.formdialogData2.proTime = ''
      }
    },
    // 服务方式1
    PlayChange1(res) {
      res == '局' || res == '次'
        ? (this.EditingData1.isDisabled = false)
        : (this.EditingData1.isDisabled = true)
      if (res == '天') {
        this.EditingData1.time = '720分钟'
        this.EditingData1.proTime = '360分钟'
      } else if (res == '小时') {
        this.EditingData1.time = '60分钟'
        this.EditingData1.proTime = '30分钟'
      } else if (res == '半小时') {
        this.EditingData1.time = '30分钟'
        this.EditingData1.proTime = '15分钟'
      } else {
        this.EditingData1.time = ''
        this.EditingData1.proTime = ''
      }
    },
    // 服务方式2
    PlayChange2(res) {
      res == '局' || res == '次'
        ? (this.EditingData2.isDisabled = false)
        : (this.EditingData2.isDisabled = true)
      if (res == '天') {
        this.EditingData2.time = '720分钟'
        this.EditingData2.proTime = '360分钟'
      } else if (res == '小时') {
        this.EditingData2.time = '60分钟'
        this.EditingData2.proTime = '30分钟'
      } else if (res == '半小时') {
        this.EditingData2.time = '30分钟'
        this.EditingData2.proTime = '15分钟'
      } else {
        this.EditingData2.time = ''
        this.EditingData2.proTime = ''
      }
    },
    // 监听服务方式的改变
    changeSer(res) {
      res == '二种服务方式' ? (this.isShow = true) : (this.isShow = false)
    },
    // 新增完成
    AddComplete() {
      this.$confirm('新增技能信息是否填写正确？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          this.dialogFormVisible1 = false
          this.$message({
            type: 'success',
            message: '新增成功!'
          })
        })
        .catch(() => {
          this.$message({
            type: 'info',
            message: '请再确认一下！'
          })
        })
    },
    // 字段编辑
    editing() {
      this.$router.push('/AccompanyCenter/Kings')
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
.dialogBox {
  .el-input {
    width: 218px !important;
  }
}
.first-item {
  margin-bottom: 8px;
  margin-top: -28px;
}
// 新建技能的模态框
.dialogMain {
  width: 500px;
  height: 400px;
  overflow: auto;
  padding-right: 15px;
}
//特色字段
.Feature {
  margin-top: 10px;
  text-align: center;
  .titleText {
    line-height: 30px;
    .teshe {
      font-size: 16px;
      font-weight: bold;
    }
  }
  // 游戏类
  .game {
    span {
      margin-right: 10px;
    }
    .switchList {
      display: flex;
      flex-wrap: wrap;
    }
    .swItem {
      width: 150px;
      margin-bottom: 15px;
    }
  }
}
//审核字段
.Audit {
  margin-top: 10px;
  text-align: center;
  .titleText {
    line-height: 30px;
    .teshe {
      font-size: 16px;
      font-weight: bold;
    }
  }
  .radio {
    margin-top: 25px;
  }
}

// 头像上传的样式
.avatar-uploader,
.el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
}
.avatar-uploader,
.el-upload:hover {
  border-color: #409eff;
  width: 104px;
  height: 104px;
}
.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 100px;
  height: 100px;
  line-height: 100px;
  text-align: center;
}
.avatar {
  width: 105px;
  height: 105px;
  display: block;
}
.selectChange {
  width: 120px;
  margin-bottom: 10px;
}
</style>
