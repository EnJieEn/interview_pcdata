<template>
  <el-container>
    <el-aside width="200px">
      <PcAside />
    </el-aside>
    <el-container>
      <el-header><PcHeader /></el-header>
      <el-main>
        <PcMain />
      </el-main>
      <el-footer><PcFooter/></el-footer>
    </el-container>
  </el-container>
</template>

<script>
import PcAside from '@/components/pc_aside.vue'
import PcHeader from '@/components/pc_header.vue'
import PcMain from '@/components/pc_main.vue'
import PcFooter from '@/components/pc_footer.vue'
export default {
  name: 'HomeView',
  components: {
    PcAside,
    PcHeader,
    PcMain,
    PcFooter
  }
}
</script>
<style scoped>
.el-header {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
  padding: 0;
}

.el-aside {
  background-color: #2a3139;
  color: #333;
  text-align: center;
  line-height: 200px;
}

.el-main {
  background-color: #F5F5F5;
  color: #333;
  padding: 0;
}

#app > .el-container {
  height: 100%;
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>
