<template>
    <div class="container mx-auto w-1/2 py-8">
        <Title>{{ post.title }} | {{ title }}</Title>
        <h3 class="text-3xl font-bold">{{ post.title }}</h3>
        <div class="post-meta text-gray-700 flex items-center space-x-2">
            <div>{{ format(new Date(post.created_at), 'MMMM dd, yyyy') }}</div>
            <div>&middot;</div>
            <div>{{ post.user.name }}</div>
        </div>
        <div class="post-content mt-4">
            {{ post.body }}
        </div>
    </div>
</template>

<script setup>
import { format, compareAsc } from 'date-fns'
const title = useState('title')
const route = useRoute()

// const { data: post } = await useFetch(`http://n3-app.test/api/posts/${route.params.id}`)
const post = await useNuxtApp().$apiFetch(`/api/posts/${route.params.id}`)
</script>