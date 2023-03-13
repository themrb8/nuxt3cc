<template>
    <div class="post-container py-8">
        <h3 class="text-3xl font-bold"><NuxtLink :to="`/posts/1`">Title of Post</NuxtLink></h3>
        <div class="post-meta text-gray-700 flex items-center space-x-2">
            <div>March 13, 2023</div>
            <div>&middot;</div>
            <div>RomanTheMrb</div>
        </div>
        <div class="post-preview leading-relaxed mt-4">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Minima molestias delectus totam aspernatur eius odio suscipit, beatae repellendus a quasi, aliquam quaerat optio porro reprehenderit?
        </div>
        <div class="mt-4">
            <NuxtLink :to="`/posts/1`" class="bg-blue-700 hover:bg-blue-800 text-white rounded inline-block px-4 py-2">Read More</NuxtLink>
        </div>
    </div>
</template>