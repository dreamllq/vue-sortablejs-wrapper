<template>
  <el-dialog
    v-model='dialogVisible'
    title='Tips'
    width='600'
  >
    <biz-table v-if='dialogVisible' />
    <template #footer>
      <span class='dialog-footer'>
        <el-button @click='dialogVisible = false'>Cancel</el-button>
        <el-button type='primary' @click='dialogVisible = false'>
          Confirm
        </el-button>
      </span>
    </template>
  </el-dialog>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import BizTable from './table.vue';

const dialogVisible = ref(false);

const show = () => {
  dialogVisible.value = true;
};

defineExpose({ show });
</script>

<style scoped>

</style>