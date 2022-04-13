<template>
  <Head title="Posts" />
  <AuthenticatedLayout>
    <template #header>
      <h2 class="font-semibold text-md leading-tight my-auto items-center justify-items-center">
        <div class="my-2">
            All Posts
        </div>
      </h2>
    </template>

    <NavLink :href="route('post.create')" class="py-1 ml-2 tracking-widest leading-10 text-gray-700 rounded border-b-2 border-transparent text-sm hover:border-teal-500 hover:text-teal-500 transition duration-150 ease-in-out focus:text-gray-500">
        <i class="fa fa-plus" aria-hidden="true"></i> Add New Post
    </NavLink>

    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
      <div class="p-3 bg-white border-b border-gray-200 px-12 py-6">

        <ValidationErrors class="mb-4" />

        <!-- <div v-if="$page.props.flash.message" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.message }}
        </div>
        <div v-if="$page.props.flash.error" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.error }}
        </div> -->

        <div v-if="posts.length" class="grid grid-cols-4 gap-7 font-medium text-sm lg:grid-cols-2">
            <!-- <ol class="list-[circle] list-inside">
                <li v-for="config in remoteConfigs" :key="config.id">
                    <ContentLink :href="route('remoteConfig.edit', config)">
                        {{ config.name }}
                    </ContentLink>
                </li>
            </ol> -->

            <!-- General Report -->
                    <div v-for="post in posts" :key="post.id" class="report-card">
                        <NavLink :href="route('post.edit', post)" class="">
                            <div class="card">
                                <div class="card-body flex flex-col hover:shadow-xl hover:shadow-teal-500">

                                    <!-- top -->
                                    <div class="flex flex-row justify-between items-center">
                                        <div class="h6 text-green-600 fad fa-sitemap"></div>
                                        <span>{{ post.name }}</span>
                                        <span class="rounded-full text-white badge bg-teal-400 text-xs">
                                            {{ post.id }}
                                        </span>
                                    </div>
                                    <!-- end top -->

                                    <!-- bottom -->
                                    <div class="mt-2">
                                        <p>Content</p>
                                        <h1 class="h5">{{ post.content }}</h1>
                                    </div>
                                    <!-- end bottom -->

                                </div>
                            </div>
                            <div class="footer bg-white p-1 mx-4 border border-t-0 rounded rounded-t-none"></div>
                        </NavLink>
                    </div>

        </div>
        <div v-else>
            <div class="py-12">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200 font-medium text-lg">
                        There is no any post yet..
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
import NavLink from "@/Components/NavLink.vue";
import { Head } from "@inertiajs/inertia-vue3";

export default {
  components: {
    AuthenticatedLayout,
    ValidationErrors,
    Head,
    NavLink,
  },

  props: {
    posts: Object,
    postCats: Object,
  },
};
</script>
