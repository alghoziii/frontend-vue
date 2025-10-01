<script setup>
import { ref, onMounted } from 'vue'
import ItemCard from "../ItemCard.vue";
import axios from 'axios';

const items = ref([])

async function getItemsData() {
    try {
        const response = await axios.get('http://127.0.0.1:8000/api/products')
        items.value = response.data.data.data
    } catch (error) {
        console.error(error)
    }
}

onMounted(() => {
    getItemsData
})
</script>
<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New items</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <ItemCard v-for="item in items" :key="item.id" :id="item.id" :title="item.name" :description="item.subtitle"
                :image="item.thumbnails" />


        </div>
    </div>
</template>
