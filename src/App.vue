
<template>
  <OrderRecord msg="這會用來顯示訂單紀錄"  v-if="false"/>
  <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
    <el-tab-pane label="User">User</el-tab-pane>
    <el-tab-pane label="Config">Config</el-tab-pane>
    <el-tab-pane label="Role">Role</el-tab-pane>
    <el-tab-pane label="Task">Task</el-tab-pane>
  </el-tabs>
</template>



<script setup>
import OrderRecord from './components/order_record.vue'
import { ref } from 'vue'
const activeName = ref('first')
const handleClick = (tab, event) => {
  console.log(tab, event)
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
}
</style>
