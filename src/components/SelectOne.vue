<template>
  <q-select
    v-if="withChange === true"
    class="col-xs-12 col-sm-6 col-md-4"
    filled
    v-model="modal"
    :options="props.options"
    label="Provinsi"
    emit-value
    map-options
    @update:model-value="(val) => onEventChange(val)"
  />
  <q-select
    v-if="withChange === false"
    class="col-xs-12 col-sm-6 col-md-4"
    filled
    v-model="modal2"
    :options="props.options"
    label="Kota"
    emit-value
    map-options
  />
</template>

<script setup lang="ts">
import { Select } from './models';
// import { api } from 'boot/axios';
import { ref } from 'vue';
interface Props {
  options?: Select[];
  // model: string;
  withChange: boolean;
}

// const props = withDefaults(defineProps<Props>(), {

// });
// const model = ref('');

// const model2 = ref('');
// const options = ref([]);

const props = withDefaults(defineProps<Props>(), {
  options: () => [],
  model: '',
});

const modal = ref('');
const modal2 = ref('');
const emit = defineEmits<{
  (e: 'updateData', id: string): void;
}>();

const onEventChange = (id: string) => {
  emit('updateData', id);
};
</script>
