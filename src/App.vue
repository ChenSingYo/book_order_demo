<template>
  <h1>Book Order UI Demo</h1>
  <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
    <el-tab-pane label="下單" name="Order">
      <Order />
    </el-tab-pane>
    <el-tab-pane label="訂單紀錄" name="OrderHistory">
      <OrderHistory />
    </el-tab-pane>
  </el-tabs>
</template>

<script>
import { ref } from 'vue'
import Order from './components/Order.vue'
import OrderHistory from './components/OrderHistory.vue'

export default {
  components: {
    OrderHistory,
    Order,
  },
  setup() {
    const activeName = ref('Order')
    const handleClick = (tab, event) => {
      console.log(tab.props.label)
    }
    return {
      activeName,
      handleClick,
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 2rem 5rem;
}

.el-tabs {
  padding: 2rem;
  box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 10%);
  -webkit-box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 10%);
  -moz-box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
  border-radius: 1rem;
}

.el-table__inner-wrapper {
  padding: 1rem 0 0 0;
  border: 1px solid var(--el-border-color-lighter);
  border-top: none;
}

.el-tabs__header {
  margin: 0;
}

/* bug: checkbox disabled狀態無法取消，得用css強制改寫 */
.el-table .el-checkbox__input.is-disabled .el-checkbox__inner {
  cursor: pointer !important;
  background-color: var(--el-checkbox-checked-bg-color) !important;
  border-color: var(--el-checkbox-checked-input-border-color) !important;
  border: var(--el-checkbox-input-border) !important;
  background-color: var(--el-checkbox-bg-color) !important;
}

.el-checkbox__inner {
  cursor: pointer !important;
}

.el-table .el-checkbox__input.is-disabled .el-checkbox__inner:hover {
  border-color: var(--el-checkbox-input-border-color-hover) !important;
}

.el-checkbox__input.is-disabled.is-indeterminate .el-checkbox__inner {
  background-color: var(--el-checkbox-checked-bg-color) !important;
  border-color: var(--el-checkbox-checked-input-border-color) !important;
}

.el-checkbox__input.is-disabled.is-indeterminate .el-checkbox__inner::before {
  background-color: white !important;
  border-color: white !important;
}

.el-checkbox__input.is-disabled.is-checked .el-checkbox__inner {
  background-color: var(--el-checkbox-checked-bg-color) !important;
  border-color: var(--el-checkbox-checked-input-border-color) !important;
}

.el-checkbox__input.is-disabled .el-checkbox__inner::after {
  cursor: pointer !important;
  border-color: white !important;
}
/* bug: checkbox disabled狀態無法取消，得用css強制改寫 */

@media screen and (max-width: 576px) {
  #app {
    padding: 1rem;
  }
}
</style>
