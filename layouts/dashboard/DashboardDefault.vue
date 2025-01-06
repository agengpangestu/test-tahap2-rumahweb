import Cookie from 'js-cookie';
<template>
    <div class="flex flex-col min-h-screen">
        <div class="bg-red-500 flex justify-between p-1 px-5 items-center w-full h-[60px]">
            <div>
                <h1>Tabler CRUD</h1>
            </div>
            <div class="space-x-4">
                <NuxtLink to="/dashboard/">List Topic</NuxtLink>
                <NuxtLink to="/dashboard/qa">QA</NuxtLink>
                <NuxtLink to="/dashboard/category">Category</NuxtLink>
                <button @click="logout">Logout</button>
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