<template>
  <Head title="Posts" />
  <AuthenticatedLayout>

    <h2 class="font-semibold text-md leading-tight my-auto items-center justify-items-center float-right absolute right-0">
        <NavLink :href="route('category.post.create', category)" class=" text-gray-900 bg-green-400 rounded-3xl px-5 py-1 font-semibold mt-5">
            Yeni İçerik Ekle +
        </NavLink>
    </h2>

    <div class="overflow-hidden">
      <div class="p-3 px-12 py-6">

        <ValidationErrors class="mb-4" />

        <div v-if="$page.props.flash.message" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.message }}
        </div>
        <div v-if="$page.props.flash.error" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.error }}
        </div>

        <div v-if="categoryPosts.length" class="grid md:grid-cols:1 lg:grid-cols-3 mt-12 gap-10">
            <div v-for="post in categoryPosts" :key="post.id" class="max-w-sm rounded overflow-hidden">
                <NavLink :href="route('post.edit', post)">
                    <img class="w-full rounded-3xl" :src="'/images/' + post.img" alt="Sunset in the mountains">
                        <div class="px-6 py-4">
                            <div class="font-bold text-xl mb-2">{{ post.title }}</div>
                            <p class="text-gray-700 text-base">
                            {{ post.content }}
                            </p>
                        </div>
                </NavLink>
            </div>
        </div>

        <!-- <div v-if="categoryPosts.length">

                    <div v-for="post in categoryPosts" :key="post.id" class="card">
                        <NavLink :href="route('post.edit', post)" class="card-body">

                            <img v-if="post.img" :src="'images/' + post.img" alt="" />
                                    <div class="text-center">
                                        {{ post.title }}<br>
                                    </div>
                                    <div class="mt-2 text-center">
                                        {{ post.content }}
                                    </div>
                        </NavLink>
                    </div>

        </div> -->
        <div v-else>
            <div class="py-12">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200 font-medium text-lg">
                        There is no any post in this category yet..
                    </div>
                </div>
            </div>
        </div>
      </div>
    </div>

  </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from "@/Layouts/Authenticated.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import NavLink from "@/Components/ResponsiveNavLink.vue";
import { Head } from "@inertiajs/inertia-vue3";

export default {
  components: {
    AuthenticatedLayout,
    ValidationErrors,
    Head,
    NavLink,
  },

  props: {
    category: Object,
    categoryPosts: Object,
  },
};
</script>
