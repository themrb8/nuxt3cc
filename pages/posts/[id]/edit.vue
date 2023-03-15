<template>
    <div class="container mx-auto w-1/2 py-8">
        <ul
        v-if="errors.length > 0"
        class="mb-4 list-disc list-inside text-sm text-red-600">
            <li v-for="(error, index) in errors" :key="index">
                {{ error }}
            </li>
        </ul>
        <h2 class="text-2xl mb-4">Edit Post</h2>
        <form action="#" class="block font-semibold" @submit.prevent="updatePost">
            <div>
                <label for="title" class="block font-semibold">Title</label>
                <input
                type="text"
                v-model="title"
                id="title"
                class="px-2 py-2 w-full shadow rounded mt-2"
                />
            </div>
            <div>
                <label for="body" class="block font-semibold mt-4">Body</label>
                <textarea
                v-model="body"
                name="body"
                id="body"
                cols="30"
                rows="10"
                class="px-2 py-2 w-full shadow rounded mt-2"
                ></textarea>
            </div>
            <div class="flex justify-between items-center">
                <button
                type="submit"
                class="inline-block bg-blue-600 hover:bg-blue-700 text-white rounded px-4 py-2"
                >Update Post</button>
                <span v-show="isLoading">Loading...</span>
                <button
                @click="deletePost"
                class="inline-block bg-red-600 hover:bg-red-700 text-white rounded px-4 py-2"
                >Delete Post</button>
            </div>
        </form>
    </div>
</template>

<script setup>
definePageMeta({
    middleware: ['auth'],
})
const title = ref('')
const body = ref('')
const isLoading = ref(false)
const errors = ref([])
const router = useRouter()
const route = useRoute()
const { $apiFetch } = useNuxtApp()
const post = ref(null)

onMounted(async() => {
    try {
        post.value = await $apiFetch(`/api/postsAuth/${route.params.id}`)
    title.value = post.value.title
    body.value = post.value.body
    } catch(err) {
        window.location.pathname = '/'
    }
})

async function updatePost() {
    isLoading.value = true
    try {
        const post = await $apiFetch(`/api/post/${route.params.id}`, {
        method: 'PATCH',
        body: {
            title: title.value,
            body: body.value,
        }
    })

    title.value = ''
    body.value = ''
    
    alert('Updated Post')
    router.push('/my-info')
    } catch(err) {
        if(err.response.status === 403){
            alert(err.data.message)
            return
        }
        errors.value = Object.values(err.data.errors).flat()
        isLoading.value = false
        }
}
async function deletePost() {
    isLoading.value = true
    try {
        const post = await $apiFetch(`/api/post/${route.params.id}`, {
        method: 'DELETE',
    })

    title.value = ''
    body.value = ''
    
    alert('Deleted Post')

    router.push('/my-info')
    } catch(err) {
        console.log(err.data)
        }
}
</script>