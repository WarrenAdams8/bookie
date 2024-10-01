<template>
    <h1>Index page</h1>
    <p>Search Query is: {{ debouncedSearchQuery }}</p>
    <input v-model="searchQuery" placeholder="search" />
    <p v-if="status == 'pending'">Loading...</p>
    <template v-else>
        <li v-for="book in books.items">
            <NuxtLink :to="{ name: 'bookDetails-id', params: { id: book.id } }">
                {{ book.volumeInfo.title }}
                <img :src=book.volumeInfo.imageLinks.smallThumbnail />
            </NuxtLink>
        </li>
    </template>
</template>
<script setup lang="ts">

const searchQuery = ref('Harry Potter')
const debouncedSearchQuery = refDebounced(searchQuery, 500)

const { data: books, status }: any = await useLazyAsyncData(
    'books',
    () => $fetch(`https://www.googleapis.com/books/v1/volumes?q=${debouncedSearchQuery.value ? debouncedSearchQuery.value : 'Harry potter'}&maxResults=30&filter=paid-ebooks`), {
    watch: [debouncedSearchQuery]
}
)

</script>
