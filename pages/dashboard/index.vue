<template>
  <div class="bg-white p-2 rounded space-y-4">
    <div class="border-b">
      <h2 class="font-semibold">Departements</h2>
    </div>
    <table class="w-full">
      <thead>
        <!-- <tr>
          <th>Departements</th>
        </tr> -->
      </thead>
      <tbody>
        <tr v-for="(item, index) in departement.list" :key="index">
          <td class="border p-2 px-3">
            <NuxtLink :to="`/dashboard/${item}`">
              {{ item }}
            </NuxtLink>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="js" setup>
import axios from 'axios';

definePageMeta({
  layout: "dashboard-default"
})

const departement = reactive({
  list: []
})


const ListData = async () => {
  try {
    const { data } = await axios.get(`https://api-topic.demo4.srs-x.net/admin/department/list`, {
      method: "GET",

    })
    departement.list = data.data

  } catch (error) {

  }
}


onMounted(() => {
  ListData();
});
</script>

<style></style>