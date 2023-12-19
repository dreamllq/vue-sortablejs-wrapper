<template>
  <div ref='tableSortWrapperRef' class='table-sort-wrapper'>
    <wrapper
      v-if='!reloadFlag'
      ref='tableWrapperRef'
      :handle='handle'
      :ghost-class='ghostClass'
      :selector='selector'
      :data='_data'
      @end='onEnd'>
      <template #default='slotScope'>
        <slot :data='slotScope.data' />
      </template>
    </wrapper>
  </div>
</template>

<script setup lang="ts">
import { nextTick, ref, watch } from 'vue';
import Wrapper from './wrapper.vue';
import { cloneDeep } from 'lodash';


const props = defineProps({
  handle: {
    type: String,
    default: undefined
  },
  ghostClass: {
    type: String,
    default: 'sortable-ghost'
  },
  data: {
    type: Array,
    default: () => ([])
  },
  selector: {
    type: String,
    default: '.el-table__body-wrapper table tbody'
  }
});

watch(() => props.data, async () => {
  reloadFlag.value = true;
  await nextTick();
  _data.value = cloneDeep(props.data);
  reloadFlag.value = false;
});


const tableWrapperRef = ref();
const reloadFlag = ref(false);
const _data = ref(cloneDeep(props.data));

const onEnd = async (e) => {
  reloadFlag.value = true;
  await nextTick();
  const tempRow = _data.value[e.oldIndex];
  _data.value.splice(e.oldIndex, 1);
  _data.value.splice(e.newIndex, 0, tempRow);
  reloadFlag.value = false;
};


const getData = () => cloneDeep(_data.value);

defineExpose({ getData });

</script>

<style scoped lang="scss">
.table-sort-wrapper {
  width: 100%;
  height: 100%;
}
</style>