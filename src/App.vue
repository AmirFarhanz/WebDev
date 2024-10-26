<script setup>
import { ref, onMounted } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');

const titleVal = ref("");
const posts = ref([])

async function Submit() {

    const data = {
        title: titleVal.value,
        description: "test",
    }

    const result = await pb.collection("posts").create(data);
    posts.value = await pb.collection("posts").getFullList();

}

onMounted(async function(){
    const result = await pb.collection("posts").getFullList();
    posts.value = result;
})

</script>

<template>

    <input v-model="titleVal" />
    <button @click="Submit">Add</button>

    <ul>
        <li v-for="post in posts">
            {{ post.title }}

        </li>
    </ul>
</template>

<style scoped></style>
