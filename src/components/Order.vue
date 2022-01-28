<template>
  <el-table :data="filterTableData">
    <el-table-column label="Item Id" prop="itemId" align="left" width="150" />
    <el-table-column label="Title" prop="title" align="left" />
    <el-table-column label="Order Quantity" prop="orderQuantity" align="center"> </el-table-column>
    <template #header>
      <el-input v-model="search" size="small" placeholder="Type to search" />
    </template>
    <el-table-column type="expand" width="120" align="right">
      <template #default="props">
        <ul>
          <li>2</li>
          <li>3</li>
          <li>4</li>
          <li>4</li>
          <li>5</li>
        </ul>
      </template>
    </el-table-column>
  </el-table>
  <el-button
    class="orderBtn"
    size="default"
    type="primary"
    @click="handleEdit(scope.$index, scope.row)"
    >下單</el-button
  >
</template>

<script setup>
import { ref, computed } from 'vue'

const search = ref('')
const filterTableData = computed(() =>
  tableData.filter(
    (data) =>
      !search.value ||
      data.name.toLowerCase().includes(search.value.toLowerCase())
  )
)
const handleEdit = (index, row) => {
  console.log(index, row)
}
const handleDelete = (index, row) => {
  console.log(index, row)
}

const tableData = [
  {
    itemId: 'B001',
    title: 'Tom & Jerry',
    orderQuantity: 1,
    item: {
      material: 'No. 189, Grove St, Los Angeles',
      desc: 'ASSY CELL M238HVN01.00D AUO',
      materialGroup: 'A01',
    },
  },
  {
    itemId: 'B002',
    title: 'Fifty Shades of Grey',
    orderQuantity: 1,
    item: {
      material: 'No. 189, Grove St, Los Angeles',
      desc: 'ASSY CELL M238HVN01.00D AUO',
      materialGroup: 'A02',
    },
  },
  {
    itemId: 'B003',
    title: 'Godfather',
    orderQuantity: 1,
    item: {
      material: 'No. 189, Grove St, Los Angeles',
      desc: 'ASSY CELL M238HVN01.00D AUO',
      materialGroup: 'A03',
    },
  },
  {
    itemId: 'B004',
    title: 'Bible',
    orderQuantity: 1,
    item: {
      material: 'No. 189, Grove St, Los Angeles',
      desc: 'ASSY CELL M238HVN01.00D AUO',
      materialGroup: 'A04',
    },
  },
]
</script>

<style scoped>
button.el-button.orderBtn {
  display: inline-block;
  margin-top: 2rem;
}
</style>
