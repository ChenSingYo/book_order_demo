<template>
  <div class="search_input">
    <el-input v-model="search" placeholder="Type to search" input-style="border-color: #909399;" />
  </div>

  <el-table show-summary :summary-method="getSummaries" :data="filterTableData">
    <el-table-column
      label="Item Id"
      prop="itemId"
      align="center"
      min-width="50"
      max-width="100"
    />
    <el-table-column label="Title" prop="title" align="left" />
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
    <el-table-column label="Quantity" align="center" width="150">
      <template #default="props">
        <el-input-number
          v-model="props.row.orderQuantity"
          @change="handleEditQuantity"
          :min="0"
          :max="100"
          controls-position="right"
          size="small"
        ></el-input-number>
      </template>
    </el-table-column>
    <el-table-column align="center" max-width="200" min-width="60" prop="price">
      <template #header> Price (NT$) </template>
      <template #default="props">{{ props.row.price }} </template>
    </el-table-column>
    <el-table-column align="center" max-width="150" min-width="100">
      <template #header> Subtotal (NT$) </template>
      <template #default="props">
        <h4>{{ props.row.orderQuantity * props.row.price }}</h4>
      </template>
    </el-table-column>
  </el-table>
  <div class="table_footer">
    <el-button
      class="order_btn"
      size="default"
      type="primary"
      @click="handleSendOrder"
      >下單</el-button
    >
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const totalCost = ref(0)
const tableData = [
  {
    itemId: 'B001',
    title: 'Tom & Jerry',
    orderQuantity: 0,
    price: 2,
    item: {
      material: 'paper',
      desc: 'pulp fiction',
      materialGroup: 'A01',
    },
  },
  {
    itemId: 'B002',
    title: 'Fifty Shades of Grey',
    orderQuantity: 0,
    price: 15,
    item: {
      material: 'paper',
      desc: 'movie script',
      materialGroup: 'A02',
    },
  },
  {
    itemId: 'B003',
    title: 'Godfather',
    orderQuantity: 0,
    price: 10,
    item: {
      material: 'paper',
      desc: 'movie script',
      materialGroup: 'A03',
    },
  },
  {
    itemId: 'B004',
    title: 'Bible',
    orderQuantity: 0,
    price: 99,
    item: {
      material: 'paper',
      desc: 'Holy Bible',
      materialGroup: 'A04',
    },
  },
]

const search = ref('')

const filterTableData = computed(() =>
  tableData.filter(
    (data) =>
      !search.value ||
      data.title.toLowerCase().includes(search.value.toLowerCase())
  )
)
const handleEditQuantity = (newVal, oldVal) => {
  console.log(newVal, oldVal)
}

const handleSendOrder = () => {
  let itemSelected = filterTableData.value.filter(
    (item) => item.orderQuantity !== 0
  )

  let showItemSelected = []
  itemSelected.forEach(
    (item) =>
      (showItemSelected +=
        '品名：' + item.title + ', 數量：' + item.orderQuantity + '\n')
  )
  alert(
    '要下單的品項：\n' + showItemSelected + '\n 訂單總額：' + totalCost.value
  )
}

const getSummaries = (param) => {
  const { columns, data } = param
  const sums = []
  columns.forEach((column, index) => {
    if (index === 4) {
      sums[index] = 'Total Cost'
      return
    }

    if (index === 5) {
      sums[index] = 0
      data.forEach((item) => (sums[index] += item.price * item.orderQuantity))
      sums[index] = `$${sums[index]}`
      totalCost.value = sums[index]
    }
  })
  return sums
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
  margin-top: 2rem;
  padding: 1rem;
}
button.el-button.order_btn {
  display: inline-block;
  margin-left: auto;
}
</style>
