<template>
  <div class="w-full min-h-screen flex justify-center items-center">
    <div class="flex flex-col justify-center space-y-4 bg-gray-500 p-5 rounded">
      <div class="flex flex-col">
        <label for="username">Username</label>
        <input type="text" name="username" id="username" v-model="vm.username">
      </div>
      <div class="flex flex-col">
        <label for="password">Password</label>
        <input type="text" name="password" id="password" v-model="vm.password">
      </div>
      <button @click="login">Login</button>
    </div>
  </div>
</template>

<script lang="js" setup>
import axios from 'axios';
import Cookie from "js-cookie";

definePageMeta({
  layout: false
})

const loading = ref(false);
const vm = reactive({
  username: "",
  password: ""
})

const login = async () => {
  try {
    const { data } = await axios.post(`https://api-topic.demo4.srs-x.net/admin/auth/login`, vm, {
      method: "POST"
    })
    console.log(data);
    Cookie.set("token", data.token);
    navigateTo("/dashboard")

  } catch (error) {
    console.log(error);

  }
}
</script>

<style></style>