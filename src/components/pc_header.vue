<template>
  <div id="header">
    <el-menu
      class="el-menu-demo"
      mode="horizontal"
      background-color="#2A3139"
      text-color="#fff"
      active-text-color="#ffd04b"
    >
      <el-menu-item
        v-for="(i, k) in headerList"
        style="border-bottom: none"
        :index="i.key"
        :key="k"
      >
        <i :class="i.icon"></i>
        <span>{{ i.text }}</span>
      </el-menu-item>
    </el-menu>
  </div>
</template>

<script>
export default {
  data () {
    return {
      headerList: [
        { icon: 'el-icon-s-home', text: '首页', key: '1' },
        { icon: 'el-icon-s-release', text: '主数据', key: '2' },
        { icon: 'el-icon-s-ticket', text: '辖区管理', key: '3' },
        { icon: 'el-icon-s-open', text: '行为管理系统', key: '4' }
      ]
    }
  }
}
</script>

<style scoped>
#header {
  background-color: #2a3139;
  padding-left: 80px;
}
</style>
