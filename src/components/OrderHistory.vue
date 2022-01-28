<template>
  <el-table
    ref="multipleTableRef"
    :data="filterTableData"
    @selection-change="handleSelectionChange"
  >
    <el-table-column type="selection" width="55" align="center">
    </el-table-column>

    <el-table-column label="Order Id" width="160" align="center">
      <template #default="singleData">{{ singleData.row.orderId }}</template>
    </el-table-column>

    <el-table-column
      property="customerName"
      label="Customer"
      width="120"
      align="center"
    />

    <el-table-column type="expand" width="55">
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

    <el-table-column property="quantity" label="Quantity" align="center" />

    <el-table-column property="totalPrice" label="Total Price" align="center" />

    <el-table-column align="right">
      <template #header>
        <el-input v-model="search" size="small" placeholder="Type to search" />
      </template>
      <template #default="singleData">
        <el-button
          size="small"
          type="danger"
          @click="handleDelete(singleData.$index, singleData.row)"
          >Delete</el-button
        >
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import { computed, ref } from 'vue'

export default {
  setup() {
    const isDisabled = ref(false)
    const search = ref('')
    const filterTableData = computed(() =>
      tableData.filter(
        (data) =>
          !search.value ||
          data.customerName.toLowerCase().includes(search.value.toLowerCase()) ||
          data.orderId.includes(search.value)
      )
    )
    const tableData = [
      {
        orderId: 'ITEM001',
        customerName: 'Mary',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM002',
        customerName: 'John',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM003',
        customerName: 'Jane',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM004',
        customerName: 'Tom',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM005',
        customerName: 'Bill',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM006',
        customerName: 'Tammy',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
      {
        orderId: 'ITEM007',
        customerName: 'Joseph',
        quantity: 5,
        totalPrice: 10,
        isSelected: false,
      },
    ]

    const multipleTableRef = ref()
    const multipleSelection = ref([])
    const toggleSelection = (rows) => {
      if (rows) {
        rows.forEach((row) => {
          // TODO: improvement typing when refactor table
          // eslint-disable-next-line
          multipleTableRef.value.toggleRowSelection(row, undefined)
        })
      } else {
        multipleTableRef.value.clearSelection()
      }
    }
    const handleSelectionChange = (val) => {
      multipleSelection.value = val
    }

    // expose to template
    return {
      search,
      tableData,
      multipleTableRef,
      multipleSelection,
      toggleSelection,
      handleSelectionChange,
      filterTableData,
      isDisabled,
    }
  },
}
</script>

<style scoped></style>
