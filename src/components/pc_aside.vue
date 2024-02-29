<template>
  <div>
    <div class="log">
      <i class="el-icon-platform-eleme"></i>
      <span>上海正也医药有限公司</span>
    </div>
    <el-row class="tac">
      <el-col>
        <el-menu
          unique-opened
          default-active="1-1-1"
          class="el-menu-vertical-demo"
          background-color="#2A3139"
          text-color="#FFFFFF"
          active-text-color="#ffd04b"
        >
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>年度协议管理</span>
            </template>
            <el-submenu index="1-1">
              <template slot="title">二级商协议</template>
              <el-menu-item index="1-1-1">新增二级商协议</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-menu-item index="2">
            <i class="el-icon-menu"></i>
            <span slot="title">功能功能B</span>
          </el-menu-item>
          <el-menu-item index="3">
            <i class="el-icon-setting"></i>
            <span slot="title">功能功能C</span>
          </el-menu-item>
          <el-menu-item index="4">
            <i class="el-icon-s-tools"></i>
            <span slot="title">功能功能D</span>
          </el-menu-item>
          <el-menu-item index="5">
            <i class="el-icon-user-solid"></i>
            <span slot="title">功能功能E</span>
          </el-menu-item>
          <el-menu-item index="6">
            <i class="el-icon-s-goods"></i>
            <span slot="title">功能功能F</span>
          </el-menu-item>
        </el-menu>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {}
</script>
<style scoped>
.tac {
  background-color: #545c64;
}
.log {
  display: flex;
  flex-direction: column;
  align-content: center;
  color: #ffffff;
  font-size: 12px;
  padding: 40px 0;
}
.log > span {
  line-height: 30px;
}
.el-icon-platform-eleme {
  font-size: 50px;
}
</style>
