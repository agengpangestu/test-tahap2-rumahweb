<template>
  <div class="w-full min-h-screen flex justify-center items-center">
    <div class="flex flex-col justify-center space-y-4 bg-gray-500 p-5 rounded">
      <div class="flex flex-col">
        <label for="category">Category</label>
        <input type="text" name="category" id="category" v-model="vm.category_id">
      </div>
      <div class="flex flex-col">
        <label for="content">Content</label>
        <input type="text" name="content" id="content" v-model="vm.content">
      </div>
      <button class="p-1 px-3 bg-green-500 text-white rounded" @click="addTopic">Submit</button>
    </div>
  </div>
</template>

<script lang="js" setup>
import axios from 'axios';
import Cookie from "js-cookie";

const vm = reactive({
  category_id: "",
  content: ""  
})

const addTopic = async () => {
  try {
    const { data } = await axios.post(`https://api-topic.demo4.srs-x.net/admin/data/create`, vm, {
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