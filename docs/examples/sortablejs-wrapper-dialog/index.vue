<template>
  <div>
    <el-button @click='onShow'>
      show
    </el-button>
  </div>
  <biz-dialog ref='dialogRef' />
</template>

<script setup lang="ts">
import { ref } from 'vue';
import BizDialog from './dialog.vue';

const dialogRef = ref();

const onShow = () => {
  dialogRef.value.show();
};
</script>

<style scoped>

</style>