<template>
  <div ref='tableSortWrapperTableWrapperRef' class='table-sort-wrapper__table-wrapper'>
    <slot ref='slot' :data='_data' />
  </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue';
import Sortable from 'sortablejs';
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
    required: true
  }
});

const emit = defineEmits(['end']);

const slot = ref();
const tableSortWrapperTableWrapperRef = ref();
const _data = ref<any[]>(cloneDeep(props.data));

let sortable: Sortable | null = null;

const setSort = ({ el, ghostClass, handle, selector }) => {
  console.log({
    el,
    ghostClass 
  });
  
  sortable = new Sortable(el.querySelector(selector), {
    sort: true,
    ghostClass,
    handle,
    animation: 150,
    onEnd: (e) => {
      
      emit('end', e);
    }
  });
};

onMounted(() => {
  setSort({
    el: tableSortWrapperTableWrapperRef.value,
    ghostClass: props.ghostClass,
    handle: props.handle,
    selector: props.selector
  });
});

onUnmounted(() => {
  sortable?.destroy();
});

const getData = () => cloneDeep(_data.value);

defineExpose({ getData });

</script>

<style scoped lang="scss">
.table-sort-wrapper {
  width: 100%;
  height: 100%;
}
</style>