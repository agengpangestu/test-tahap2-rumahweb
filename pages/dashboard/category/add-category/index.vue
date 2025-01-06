<template>
  <div class="w-full min-h-screen flex justify-center items-center">
    <div class="flex flex-col justify-center space-y-4 bg-gray-500 p-5 rounded">
      <div class="flex flex-col">
        <label for="department">Department</label>
        <input type="text" name="department" id="department" v-model="vm.department">
      </div>
      <div class="flex flex-col">
        <label for="name">Name</label>
        <input type="text" name="name" id="name" v-model="vm.name">
      </div>
      <button class="p-1 px-3 bg-green-500 text-white rounded" @click="addCategory">Submit</button>
    </div>
  </div>
</template>

<script lang="js" setup>
import axios from 'axios';
import Cookie from "js-cookie";

const vm = reactive({
  username: "",
  password: ""
})

const addCategory = async () => {
  try {
    const { data } = await axios.post(`https://api-topic.demo4.srs-x.net/admin/categories/create`, vm, {
      method: "POST"
    })
    console.log(data);
    Cookie.set("token", data.token);
    navigateTo("/dashboard/teknis")

  } catch (error) {
    console.log(error);
  }
}
</script>

<style></style>