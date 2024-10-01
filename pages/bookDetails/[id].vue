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
const route = useRoute()

const { data: book, status }: any = await useLazyAsyncData(
    'bookDetails',
    () => $fetch(`https://www.googleapis.com/books/v1/volumes/${route.params.id}`)
)
</script>