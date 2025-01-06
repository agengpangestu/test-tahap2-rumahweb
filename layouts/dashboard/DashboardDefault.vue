import Cookie from 'js-cookie';
<template>
    <div class="flex flex-col min-h-screen">
        <div class="bg-white flex justify-between p-1 px-5 items-center w-full h-[60px]">
            <div>
                <h1>Tabler CRUD</h1>
            </div>
            <div class="space-x-4">
                <button class="outline-gray-300 outline p-1 text-gray-300 rounded">
                    <NuxtLink to="/dashboard/">List Topic</NuxtLink>
                </button>
                <button class="outline-blue-500 outline p-1 rounded text-blue-500">
                    <NuxtLink to="/dashboard/qa">QA</NuxtLink>
                </button>
                <button class="outline-green-300 outline p-1 rounded text-green-500">
                    <NuxtLink to="/dashboard/category">Category</NuxtLink>
                </button>
                <button class="bg-red-500 text-white p-1 rounded" @click="logout">Logout</button>
            </div>
        </div>
        <div class="bg-gray-200 p-3 h-screen">
            <NuxtPage />
        </div>
    </div>
</template>

<script setup>
import Cookie from "js-cookie";

const logout = async () => {
    try {
        Cookie.remove("token");
        navigateTo("/login");
    } catch (error) {
        console.log(error);

    }
}
</script>

<style lang="scss" scoped></style>