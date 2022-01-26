<template>
  <h1>Book Order UI Demo</h1>
  <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
    <el-tab-pane label="List">
      <OrderRecord />
    </el-tab-pane>
    <el-tab-pane label="Order Record">
      <ItemList />
    </el-tab-pane>
  </el-tabs>
</template>

<script setup>
import OrderRecord from './components/OrderRecord.vue'
import ItemList from './components/ItemList.vue'
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
  padding: 2rem 5rem;
}

.el-tab-pane {
  border: 1px solid red;
}

@media screen and (max-width: 576px) {
  #app {
    padding: 1rem;
  }
}
</style>
