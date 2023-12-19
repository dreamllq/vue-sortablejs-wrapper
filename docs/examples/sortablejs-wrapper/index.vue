<template>
  <div>
    <el-button @click='getData'>
      getData
    </el-button>

    <el-button @click='getTable'>
      getTable
    </el-button>
  </div>

  <sortablejs-wrapper
    ref='tableSortablejsWrapperRef'
    handle='.handle-drag'
    selector='.el-table__body-wrapper table tbody'
    :data='tableData'>
    <template #default='{data}'>
      <el-table
        id='dragTable'
        ref='tableRef'
        :data='data'
        border
        style='width: 800px;'>
        <el-table-column prop='date' label='Date' width='180' />
        <el-table-column prop='name' label='Name' width='180' />
        <el-table-column prop='address' label='Address' />
        <el-table-column label='操作' width='100'>
          <template #default>
            <div class='handle-drag'>
              <el-icon>
                <sort />
              </el-icon>
            </div>
          </template>
        </el-table-column>
      </el-table>
    </template>
  </sortablejs-wrapper>
</template>

<script setup lang="ts">
import { SortablejsWrapper } from '@/index.ts';
import { computed, ref } from 'vue';


const tableRef = ref();
const tableSortablejsWrapperRef = ref();
const tableData = [
  {
    date: '2016-05-03',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-02',
    name: 'Cilly',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-04',
    name: 'Linda',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-01',
    name: 'John',
    address: 'No. 189, Grove St, Los Angeles'
  }
];

const columns = computed(() => {
  let str = JSON.stringify(tableRef.value?.context.store.states.columns.value);
  return str;
});

const getData = () => {
  const data = tableSortablejsWrapperRef.value.getData();
  console.log(data);
};

const getTable = () => {
  console.log(tableRef.value.context);
};
</script>

<style scoped>

</style>