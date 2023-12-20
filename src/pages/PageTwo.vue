<template>
  <q-page>
    <div class="row justify-center q-mt-lg">
      <select-one :with-change="false" :options="options2"> </select-one>
    </div>
    <div class="flex justify-center q-mt-lg">
      <q-btn to="/" label="To Home" outline color="blue" />
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { City } from 'components/models';
import SelectOne from 'components/SelectOne.vue';
import { api } from 'boot/axios';
import { ref } from 'vue';

const options2 = ref([]);

const idKota = localStorage.getItem('kota_id') ?? '';

const getCity = (id: string) => {
  console.log('id', id);
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
getCity(idKota);
</script>
