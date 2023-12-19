<template>
  <sortablejs-wrapper
    handle='.handle-drag'
    :data='tableData'
    selector='.el-table__body-wrapper table tbody'
    @end='onEnd'>
    <template #default='slotScope'>
      <el-table
        id='dragTable'
        :data='slotScope.data'
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

const onEnd = (e, data) => {
  console.log(e, data);
};
</script>

<style scoped>

</style>