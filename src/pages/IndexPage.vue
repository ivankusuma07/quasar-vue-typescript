<template>
  <q-page class="justify-center">
    <div class="row justify-center q-mt-lg">
      <select-one :with-change="true" :options="options" @update-data="getCity">
      </select-one>
    </div>

    <div class="row justify-center q-mt-lg">
      <select-one :with-change="false" :options="options2"> </select-one>
    </div>
    <div class="flex justify-center q-mt-lg">
      <q-btn to="/page2" label="To Page 2" outline color="blue" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { Province, City } from 'components/models';
import { api } from 'boot/axios';
import SelectOne from 'components/SelectOne.vue';
import { ref } from 'vue';

const options = ref([]);
const options2 = ref([]);

const getProvince = () => {
  api
    .get('/api/provinces.json')
    .then((response) => {
      const dataMapped = response.data.map((items: Province) => ({
        label: items.name,
        value: items.id,
      }));
      options.value = dataMapped;
      // console.log(dataMapped);
    })
    .catch((error) => {
      console.log(error);
    });
};
getProvince();
const getCity = (id: any) => {
  // console.log('id', id);
  localStorage.setItem('kota_id', id);
  api
    .get(`/api/regencies/${id}.json`)
    .then((response) => {
      const dataMapped = response.data.map((items: City) => ({
        label: items.name,
        value: items.id,
      }));
      options2.value = dataMapped;
      // console.log(dataMapped);
    })
    .catch((error) => {
      console.log(error);
    });
};
</script>
