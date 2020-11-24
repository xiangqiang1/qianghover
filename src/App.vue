<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
.el-dialog__wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.box-card {
  margin: 15px;
}
// 分页的外边距
.pagination {
  margin: 20px 0;
}
// 模态框title的样式
.el-dialog__title {
  font-weight: bold !important;
  font-size: 22px;
}

</style>

