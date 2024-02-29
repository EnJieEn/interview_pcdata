<template>
  <div id="main">
    <!-- 面包屑区域 -->
    <div class="main_top">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item>首页</el-breadcrumb-item>
        <el-breadcrumb-item>年度协议管理</el-breadcrumb-item>
        <el-breadcrumb-item>二级商协议</el-breadcrumb-item>
        <el-breadcrumb-item>新增二级商协议</el-breadcrumb-item>
      </el-breadcrumb>
      <span>新增二级商协议</span>
    </div>
    <!-- 主体区域 -->
    <div class="main_centent">
      <!-- 模块1 -->
      <el-divider><span class="number">1</span><b>协议主体</b></el-divider>
      <div class="card_one">
        <el-form label-width="100px" :inline="true" label-position="right">
          <el-form-item label="协议客户:" required
            ><el-select
              placeholder="选择客户"
              v-model="value"
              size="small"
              style="width: 59%"
            >
              <el-option
                v-for="item in client"
                :key="item.value"
                :label="item.label"
                :value="item.label"
              >
              </el-option>
            </el-select>
            <span>{{ value }}</span>
          </el-form-item>
          <el-form-item label="协议状态:">
            <el-select v-model="state" placeholder="活动区域" size="small">
              <el-option label="正常" value="true"></el-option>
              <el-option label="有误" value="false"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="购进指标:">
            <el-select
              v-model="buyingIn"
              placeholder="请选择"
              size="small"
              style="width: 30%"
            >
              <el-option label="金额" value="sum"></el-option>
              <el-option label="数量" value="quantity"></el-option>
            </el-select>
            <el-input
              v-model="buyingInAmount"
              size="small"
              placeholder="输入金额/数量"
            />
          </el-form-item>
          <el-form-item label="纯销指标:">
            <el-button size="small">金额</el-button>
            <el-input
              v-model="marketAmount"
              size="small"
              placeholder="输入金额/数量"
            />
          </el-form-item>
          <el-form-item label="销售区域:">
            <el-button size="small">选择区域</el-button>
            <el-select
              v-model="area"
              placeholder="请选择"
              size="small"
              style="width: 30%"
            >
              <el-option label="全国" value="nationwide"></el-option>
              <el-option label="省会" value="province"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="签订时间:">
            <el-date-picker
              style="width: 100%"
              v-model="dateValue"
              type="datetime"
              placeholder="选择日期时间"
            >
            </el-date-picker>
          </el-form-item>
          <el-form-item label="购进渠道:" class="channel">
            <el-select v-model="channel" placeholder="活动区域" size="small">
              <el-option label="指定渠道" value="specified"></el-option>
              <el-option label="自由渠道" value="freedom"></el-option>
            </el-select>
            <el-button size="small">请选择渠道</el-button>
            <el-table
              :data="channelList"
              :header-cell-style="{
                background: '#F8F8F8',
                'line-hight': '50px',
              }"
            >
              <el-table-column prop="code" label="指定渠道编码" >
              </el-table-column>
              <el-table-column prop="name" label="指定渠道名称" >
              </el-table-column>
              <el-table-column prop="area" label="所在省"> </el-table-column>
            </el-table>
          </el-form-item>
        </el-form>
      </div>
      <!-- 模块2 -->
      <el-divider><span class="number">2</span><b>产品政策</b></el-divider>
      <div class="cara_two_text">
        <el-button size="small" type="primary">添加产品</el-button>
        <span
          >购进总指标（万元）：<b>{{ productPolicy.target }}</b></span
        >
        <span
          >指标按季度分解(万元): <b>{{ productPolicy.quarter }}</b></span
        >
        <span
          >纯销总指标(万元): <b>{{ productPolicy.allAmount }}</b></span
        >
      </div>
      <div class="card_one">
        <el-form class="cara_two_form">
          <el-form-item label="产品:"
            ><el-select
              placeholder="选择产品"
              v-model="product"
              size="small"
              style="width: 55%"
            >
              <el-option
                v-for="item in productList"
                :key="item.value"
                :label="item.label"
                :value="item.label"
              >
              </el-option>
            </el-select>
            <span class="product_span">{{ product }}</span>
          </el-form-item>
          <el-form-item label="签订时间:">
            <el-date-picker
              v-model="signingDate"
              type="daterange"
              range-separator="~"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
            >
            </el-date-picker>
          </el-form-item>
          <el-button size="small" type="danger">删除</el-button>
        </el-form>
        <div class="cara_two_table">
          <el-table
            class="table_one"
            :data="tableOneData"
            :header-cell-style="{
              background: '#F8F8F8',
              'border-bottom': '1px solid #bbbbbb',
            }"
          >
            <el-table-column prop="code" label="协议价（元）">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.negotiatedPrice"
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="票折(元)">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.TicketDiscount"
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="购进指标量(大单位)">
              <template slot-scope="scope">
                <el-input placeholder="请输入" v-model="scope.row.buyBig" />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="购进指标量(小单位)">
              <template slot-scope="scope">
                <el-input placeholder="请输入" v-model="scope.row.buySmall" />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="购进金额(万元)">
              <template slot-scope="scope">
                <el-input placeholder="请输入" v-model="scope.row.buyAmount" />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="纯销指标量(小单位)">
              <template slot-scope="scope">
                <el-input placeholder="请输入" v-model="scope.row.NetSaleNum" />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="纯销指标金额(万元)">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.NetSaleAmount"
                />
              </template>
            </el-table-column>
          </el-table>
          <el-table
            class="table_two"
            :data="tableOneData"
            :header-cell-style="{
              background: '#F8F8F8',
              'border-bottom': '1px solid #bbbbbb',
            }"
          >
            <el-table-column prop="code" label="分销奖励">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.negotiatedPrice"
                  size="small"
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="费用科目">
              <template slot-scope="scope">
                <el-select
                  v-model="scope.row.TicketDiscountA"
                  placeholder="请选择"
                  size="small"
                >
                  <el-option label="单选项1" value="1"></el-option>
                  <el-option label="多选项2" value="2"></el-option>
                </el-select>
              </template>
            </el-table-column>
            <el-table-column prop="name" label="零售配送">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.buyBig"
                  size="small"
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="费用科目">
              <template slot-scope="scope">
                <el-select
                  v-model="scope.row.buySmallA"
                  placeholder="请选择"
                  size="small"
                >
                  <el-option label="多选项1" value="1"></el-option>
                  <el-option label="多选项2" value="2"></el-option>
                  <el-option label="多选项3" value="3"></el-option>
                </el-select>
              </template>
            </el-table-column>
            <el-table-column prop="name" label="医疗配送商">
              <template slot-scope="scope">
                <el-input
                  placeholder="请输入"
                  v-model="scope.row.buyAmount"
                  size="small"
                />
              </template>
            </el-table-column>
            <el-table-column prop="name" label="费用科目">
              <template slot-scope="scope">
                <el-select
                  v-model="scope.row.NetSaleNumA"
                  placeholder="请选择"
                  size="small"
                >
                  <el-option label="多选项1" value="1"></el-option>
                  <el-option label="多选项2" value="2"></el-option>
                  <el-option label="多选项3" value="3"></el-option>
                </el-select>
              </template>
            </el-table-column>
            <el-table-column prop="name" label="自定义7">
              <template slot-scope="scope">
                <el-date-picker
                  v-model="scope.row.NetSaleAmount"
                  type="date"
                  size="small"
                  placeholder="选择日期"
                >
                </el-date-picker>
              </template>
            </el-table-column>
            <el-table-column prop="name" label="自定义8">
              <template slot-scope="scope">
                <el-date-picker
                  v-model="scope.row.custom"
                  type="date"
                  size="small"
                  placeholder="选择日期"
                >
                </el-date-picker>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <!-- 模块3 -->
      <el-divider><span class="number">3</span><b>补充协议</b></el-divider>
      <div class="card_three">
        <el-tabs
          v-model="editableTabsValue"
          type="card"
          editable
          @edit="handleTabsEdit"
        >
          <el-tab-pane
            :key="index"
            v-for="(item, index) in editableTabs"
            :label="item.title"
            :name="item.name"
          >
            {{ item.content }}
            <el-input
            class="card_three_textarea"
              type="textarea"
              :autosize="{ minRows: 4, maxRows: 8 }"
              v-model="textarea2"
            >
            </el-input>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      client: [
        {
          value: '1',
          label: '中国正也医药有限公司'
        },
        {
          value: '2',
          label: '中国仁爱医药有限公司'
        }
      ],
      value: '',
      state: '',
      buyingIn: '',
      buyingInAmount: '',
      marketAmount: '',
      area: '',
      dateValue: '',
      channel: '',
      channelList: [
        { code: 'BJ000090', name: '宁波九州通药业有限公司', area: '浙江省' },
        { code: 'BJ000091', name: '国药控股精华有限公司', area: '浙江省' },
        { code: 'BJ000092', name: '老百姓药业有限公司', area: '浙江省' }
      ],
      productPolicy: {
        target: '￥152.65',
        quarter: '【Q1】¥12.5，【Q2】¥12.5，【Q3】¥12.5，【Q4】¥12.5',
        allAmount: '￥152.65'
      },
      product: '',
      productList: [
        { value: 'MF', label: '美复胶丸 24粒/盒' },
        { value: 'GK', label: '感康胶丸 24粒/盒' }
      ],
      signingDate: '',
      tableOneData: [
        {
          negotiatedPrice: '',
          TicketDiscount: '',
          buyBig: '',
          buySmall: '',
          buyAmount: '',
          NetSaleNum: '',
          NetSaleAmount: ''
        }
      ],
      tableTwoData: [
        {
          negotiatedPrice: '',
          TicketDiscountA: '',
          buyBig: '',
          buySmallA: [],
          buyAmount: '',
          NetSaleNumA: [],
          NetSaleAmount: '',
          custom: ''
        }
      ],
      editableTabsValue: '1',
      editableTabs: [
        {
          title: '补充协议1',
          name: '1',
          content: '协议内容:'
        },
        {
          title: '补充协议2',
          name: '2',
          content: '协议内容:'
        },
        {
          title: '补充协议3',
          name: '3',
          content: '协议内容:'
        }
      ],
      textarea2: '',
      tabIndex: 3
    }
  },
  methods: {
    handleTabsEdit (targetName, action) {
      if (action === 'add') {
        const newTabName = ++this.tabIndex + ''
        this.editableTabs.push({
          title: '补充协议' + newTabName,
          name: newTabName,
          content: '协议内容:'
        })
        this.editableTabsValue = newTabName
      }
      if (action === 'remove') {
        const tabs = this.editableTabs
        let activeName = this.editableTabsValue
        if (activeName === targetName) {
          tabs.forEach((tab, index) => {
            if (tab.name === targetName) {
              const nextTab = tabs[index + 1] || tabs[index - 1]
              if (nextTab) {
                activeName = nextTab.name
              }
            }
          })
        }
        this.editableTabsValue = activeName
        this.editableTabs = tabs.filter((tab) => tab.name !== targetName)
      }
    }
  }
}
</script>

<style scoped>
.main_top {
  background-color: #ffffff;
  padding: 20px;
  text-align: left;
}
.el-breadcrumb {
  margin-bottom: 15px;
}
.main_centent {
  padding: 0 15px;
}
.el-divider--horizontal {
  background: 0 0;
  border-top: 2px dashed#e8eaec;
}

.el-divider--horizontal > .el-divider__text {
  display: flex;
  align-items: center;
  justify-items: center;
  background-color: #f5f5f5;
  font-size: 20px;
}
.number {
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: #4c8dfe;
  color: #ffffff;
  margin-right: 5px;
  text-align: center;
}
.card_one {
  background-color: #ffffff;
  width: 100%;
  padding: 15px 0;
  border-radius: 15px;
}
.card_one > .el-form {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.card_one > .el-form > .el-form-item {
  display: flex;
  width: 48%;
  margin-bottom: 10px;
}
.el-form-item > .el-form-item__content > .el-input {
  width: 48%;
}
.channel {
  width: 100% !important;
}
.channel /deep/ .el-form-item__content {
  width: 98%;
}
.cara_two_text {
  font-size: 13px;
  margin-bottom: 15px;
}
.cara_two_text > span {
  margin: 0 20px;
}
.product_span {
  color: #4c8dfe;
}
.cara_two_form {
  display: flex;
  align-items: center;
  justify-items: center;
  padding: 0 10px;
  border-bottom: 2px solid #bbbbbb;
}
.cara_two_table {
  padding: 10px;
}
.cara_two_table /deep/.table_one {
  border: 1px solid #bbbbbb;
  margin-bottom: 15px;
}
.card_three{
  margin-bottom: 30px;
}
.card_three > .el-tabs {
  background-color: #ffffff;
}
.card_three > .el-tabs  /deep/ .el-tabs__content{
  padding: 15px;
}
 .card_three_textarea{
  margin: 10px 0;
}
 .card_three_textarea /deep/ .el-textarea__inner{
  background-color: #F5F5F5;
}
</style>
