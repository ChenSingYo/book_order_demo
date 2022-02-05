<template>
  <div class="search_input">
    <el-input
      v-model="search"
      placeholder="Type to search"
      input-style="border-color: #909399;"
    />
  </div>

  <el-table
    ref="multipleTableRef"
    :data="filterTableData"
    @selection-change="handleSelectionChange"
  >
    <el-table-column
      type="selection"
      width="55"
      align="center"
      @change="toggleSelection"
    />

    <el-table-column
      label="Item Id"
      prop="itemId"
      align="center"
      min-width="80"
      max-width="100"
    />
    <el-table-column label="Title" prop="title" align="left" min-width="120" />

    <el-table-column type="expand" align="center" width="70">
      <template #header> Detail </template>
      <template #default="props">
        <ul>
          <li>material: {{ props.row.item.material }}</li>
          <li>desc: {{ props.row.item.desc }}</li>
          <li>materialGroup: {{ props.row.item.materialGroup }}</li>
        </ul>
      </template>
    </el-table-column>

    <el-table-column align="center" max-width="200" min-width="60" prop="price">
      <template #header> Price (NT$) </template>
      <template #default="props">{{ props.row.price }} </template>
    </el-table-column>

    <el-table-column
      label="Quantity"
      align="center"
      width="90"
      prop="orderQuantity"
    />

    <el-table-column align="center" max-width="150" min-width="120">
      <template #header> Total (NT$) </template>
      <template #default="props">
        <h4>{{ props.row.orderQuantity * props.row.price }}</h4>
      </template>
    </el-table-column>
    <el-table-column
      align="center"
      max-width="150"
      min-width="110"
      prop="timeStamp"
    >
      <template #header> Date </template>
    </el-table-column>
  </el-table>
  <div class="table_footer">
    <el-button
      class="delete_btn"
      type="danger"
      :disabled="multipleSelection.length == 0"
      @click="deleteOrderRecord(multipleSelection)"
      >刪除紀錄</el-button
    >
  </div>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
const props = defineProps(['itemOrdered'])

let filterTableData = ref([])
const isDisabled = ref(false)
const search = ref('')

let tableData = ref([
  {
    itemId: 'B001',
    title: 'Tom & Jerry',
    orderQuantity: 5,
    price: 2,
    item: {
      material: 'paper',
      desc: 'pulp fiction',
      materialGroup: 'A01',
    },
    timeStamp: '2022/1/1',
  },
  {
    itemId: 'B002',
    title: 'Fifty Shades of Grey',
    orderQuantity: 2,
    price: 15,
    item: {
      material: 'paper',
      desc: 'movie script',
      materialGroup: 'A02',
    },
    timeStamp: '2022/1/1',
  },
  {
    itemId: 'B003',
    title: 'Godfather',
    orderQuantity: 4,
    price: 10,
    item: {
      material: 'paper',
      desc: 'movie script',
      materialGroup: 'A03',
    },
    timeStamp: '2022/1/2',
  },
  {
    itemId: 'B004',
    title: 'Bible',
    orderQuantity: 3,
    price: 99,
    item: {
      material: 'paper',
      desc: 'Holy Bible',
      materialGroup: 'A04',
    },
    timeStamp: '2022/1/2',
  },
])

watch(
  () => props.itemOrdered,
  () => {
    console.log('itemOrdered@props:', props.itemOrdered)
    props.itemOrdered.forEach((item) => {
      tableData.value.push(item)
    })
    console.log('tableData@OrderHistory:', tableData)
  }
)

filterTableData = computed(() =>
  tableData.value.filter(
    (item) =>
      !search.value ||
      item.title.toLowerCase().includes(search.value.toLowerCase()) ||
      item.itemId.includes(search.value)
  )
)

// select and delete row

const multipleTableRef = ref()
const multipleSelection = ref([])

const toggleSelection = (rows) => {
  if (rows) {
    rows.forEach((row) => {
      multipleTableRef.value.toggleRowSelection(row, undefined)
    })
  } else {
    multipleTableRef.value.clearSelection()
  }
}
const handleSelectionChange = (val) => {
  multipleSelection.value = val
}

const deleteOrderRecord = (selection) => {
  console.log('delete!', selection)

  tableData.value = tableData.value.filter((item) => {
    if (
      selection.filter(
        (selcItem) =>
          selcItem.timeStamp !== item.timeStamp ||
          selcItem.itemId !== item.itemId
      ).length > 0
    ) {
      return true
    } else {
      return false
    }
  })
  console.log(tableData.value)
}
</script>

<style scoped>
.search_input {
  position: absolute;
  z-index: 10;
  top: 1rem;
  right: 1rem;
}
.table_footer {
  display: flex;
  margin-top: 1rem;
  padding: 1rem;
}
button.el-button.delete_btn {
  display: inline-block;
  margin-left: auto;
}
</style>
