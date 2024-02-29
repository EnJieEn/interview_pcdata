<template>
  <div>
    <el-button type="primary" @click="save">保存</el-button>
  </div>
</template>

<script>
export default {
  methods: {
    save () {
      alert('确定提交么？')
    }
  }
}
</script>

<style scoped></style>
