<template>
    <h1>Book Details</h1>
    <h1 v-if="status == 'pending'">Loading..</h1>
    <template v-else>
        <h3>{{ book.volumeInfo.title }}</h3>
        <img :src=book.volumeInfo.imageLinks.smallThumbnail />
        <p>{{ book.volumeInfo.description }}</p>
    </template>
</template>
<script setup lang="ts">
const nuxtApp = useNuxtApp()
const { id } = useRoute().params

const { data: book, status }: any = await useLazyAsyncData(
    `bookDetails:${id}`,
    () => $fetch(`https://www.googleapis.com/books/v1/volumes/${id}`), {
    getCachedData(key) {
        return nuxtApp.payload.data[key] || nuxtApp.static.data[key]
    },
}
)


//implement fetch at TTL logic in types


// https://nuxt.com/docs/api/composables/use-nuxt-data
// https://www.youtube.com/watch?v=mv0WcBABcIk useState instead of pinia
</script>