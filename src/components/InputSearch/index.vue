<template>
  <div class="inputSearch-container">
    <el-input v-model="inputData" placeholder="请输入分组名称" style="width: 200px;" />
    <el-button icon="el-icon-search" />
    {{ data }}
  </div>
</template>

<script>
export default {
  data() {
    return {

    }
  }
  // props: ['inputData']
}
</script>

<style scoped>
</style>
