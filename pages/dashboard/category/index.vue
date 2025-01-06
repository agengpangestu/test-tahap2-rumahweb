<template>
  <div class="bg-white p-2 rounded space-y-4">
    <div class="border-b flex justify-between p-2 px-3 items-center">
      <h2 class="font-semibold">Categories</h2>
      <button class="p-1 px-3 bg-blue-500 text-white rounded">
        <NuxtLink to="/dashboard/category/add-category">Add Category</NuxtLink>
      </button>
    </div>
    <table class="w-full">
      <thead class="border p-2 px-3">
        <tr>
          <th class="border p-2 px-3">ID</th>
          <th class="border p-2 px-3">DEPARTMENT</th>
          <th class="border p-2 px-3">NAME</th>
          <th class="border p-2 px-3">ACTION</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border p-2 px-3" v-for="(item, index) in department.list.result" :key="index">
          <td class="border p-2 px-3">
            {{ item.id }}
          </td>
          <td class="border p-2 px-3">
            {{ item.department }}
          </td>
          <td class="border p-2 px-3">
            {{ item.name }}
          </td>
          <td class="border p-2 px-3">
            ACTION
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="department.list.length" class="flex justify-center">
      <vue-awesome-paginate @click="paginate" :total-items="department.per_page"
        v-model="department.current_page"></vue-awesome-paginate>
    </div>
  </div>
</template>

<script lang="js" setup>
import axios from 'axios';

definePageMeta({
  layout: "dashboard-default"
})

const department = reactive({
  list: [],
  current_page: 1,
  first_page: 0,
  last_page: 0,
  path: "https://api-topic.demo4.srs-x.net/admin/categories/list",
  per_page: 10,
  total_data: 0,
  total_page: 0
})

const paginate = (page) => {
  department.current_page = page;
  ListData();
}

const ListData = async () => {
  try {
    const { data } = await axios.get(`https://api-topic.demo4.srs-x.net/admin/categories/list?page=${department.current_page}`, {
      method: "GET",

    })
    department.list = data.data
    department.total_data = data.data.total
    department.total_page = data.data.pagination.pagination.total_page
    department.total_page = data.data.pagination.pagination.per_page
    console.log(department.list);

  } catch (error) {

  }
}

onMounted(() => {
  ListData();
});
</script>

<style></style>