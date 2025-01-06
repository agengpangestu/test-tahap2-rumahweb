<template>
  <div class="bg-white p-2 rounded space-y-4">
    <div class="border-b flex justify-between p-2 px-3 items-center">
      <h2 class="font-semibold">Teknis</h2>
      <div class="space-x-4">
        <button class="p-1 px-3 bg-blue-500 text-white rounded">
          <NuxtLink to="/dashboard/">Back to Departments</NuxtLink>
        </button>
        <button class="p-1 px-3 bg-blue-500 text-white rounded">
          <NuxtLink to="/dashboard/teknis/add-topic">Add Topics</NuxtLink>
        </button>
      </div>
    </div>
    <table class="w-full">
      <thead class="border p-2 px-3">
        <tr>
          <th class="border p-2 px-3">ID</th>
          <th class="border p-2 px-3">DEPARTMENT</th>
          <th class="border p-2 px-3">CATEGORY</th>
          <th class="border p-2 px-3">CONTENT</th>
          <th class="border p-2 px-3">ACTION</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border p-2 px-3" v-for="(item, index) in department.list.result" :key="index">
          <td class="border p-2 px-3">
            {{ item.id }}
          </td>
          <td class="border p-2 px-3">
            Teknis
          </td>
          <td class="border p-2 px-3">
            {{ item.category }}
          </td>
          <td class="border p-2 px-3">
            {{ item.content }}
          </td>
          <td class="border p-2 px-3">
            <div class="flex space-x-2">
              <button class="px-3 p-2 bg-orange-500 text-white">Edit</button>
              <button class="px-3 p-2 bg-red-500 text-white">Delete</button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="department.list.length" class="flex justify-center">
      <vue-awesome-paginate @click="paginate" :total-items="department.per_page" v-model="department.current_page" />
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
  path: "https://api-topic.demo4.srs-x.net/admin/data/list",
  per_page: 10,
  total_data: 0,
  total_page: 0
})

const paginate = (page) => {

}

const ListData = async () => {
  try {
    const { data } = await axios.get(`https://api-topic.demo4.srs-x.net/admin/data/list?page=${department.current_page}`, {
      method: "GET",

    })
    department.list = data.data
    // department.total_data = data.data.total
    // department.total_page = data.data.pagination.pagination.total_page
    // department.total_page = data.data.pagination.pagination.per_page
    console.log(department.list);

  } catch (error) {

  }
}

onMounted(() => {
  ListData();
});
</script>

<style></style>