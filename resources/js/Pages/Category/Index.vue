<template>
  <Head title="Posts" />
  <AuthenticatedLayout>

    <div class="overflow-hidden">
      <div class="p-3 px-12 py-6">

        <ValidationErrors class="mb-4" />

        <div v-if="$page.props.flash.message" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.message }}
        </div>
        <div v-if="$page.props.flash.error" class="mb-4 font-medium text-sm text-green-600">
          {{ $page.props.flash.error }}
        </div>

        <div class="text-center text-3xl font-serif font-medium tracking-wider">
            <h1 class="text-gray-600">Kategori İşlemleri</h1>
        </div>

        <div v-if="categories.length" class="gap-7 font-medium text-sm">

            <!-- General Report -->
                    <div v-for="category in categories" :key="category.id" class="">
                        <NavLink :href="route('category.show', category)" class="ps-5">
                            <!-- top -->
                            <div class="flex flex-row justify-between items-center">
                                <span class=" text-2xl text-gray-900">{{ category.name }}</span>
                            </div>
                            <!-- end top -->
                        </NavLink>
                        <div class="float-right pe-5">
                            <NavLink :href="route('category.edit', category)" class="">

                            <!-- top -->
                            <div class="flex flex-row justify-between items-center rounded-full bg-cyan-900 px-5 py-1 text-white">
                                <span>Düzenle</span>
                            </div>
                        </NavLink>
                        <Button @click="delCategory(category)" class="">
                            <!-- top -->
                            <div class="flex flex-row justify-between items-center rounded-full bg-red-600 px-5 py-1 text-white">
                                <span>Sil</span>
                            </div>
                        </Button>
                        </div>

                        <div class="footer border border-b-1 border-gray-500 rounded rounded-t-none"></div>

                    </div>

        </div>
        <div v-else>
            <div class="py-12">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200 font-medium text-lg">
                        There is no any category yet..
                    </div>
                </div>
            </div>
        </div>

        <h2 class="font-semibold text-md leading-tight my-auto items-center justify-items-center ">
            <NavLink :href="route('category.create')" class=" text-gray-900 bg-green-400 rounded-3xl px-5 py-1 font-semibold mt-5">
                Yeni Kategori Ekle +
            </NavLink>
        </h2>

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
    categories: Object,
  },
    methods: {
        delCategory(category) {
            if (confirm('Are you sure you want to delete this Category?')) {
                this.$inertia.delete(this.route("category.destroy", category));
            }
        },
    },
};
</script>
