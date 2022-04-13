


<template>
  <Head title="NewCategory" />
  <AuthenticatedLayout>

    <div class="py-12">
        <div class="overflow-hidden">
          <div class="p-6">
            <ValidationErrors class="mb-4" />
<!--
            <div v-if="$page.props.flash.message" class="mb-4 font-medium text-sm text-green-600">
              {{ $page.props.flash.message }}
            </div>
            <div v-if="$page.props.flash.error" class="mb-4 font-medium text-sm text-green-600">
              {{ $page.props.flash.error }}
            </div> -->

            <div class="text-center text-3xl font-serif font-medium tracking-wider">
                <h1 class="text-gray-600">Yeni Kategori</h1>
            </div>

            <form @submit.prevent="submit" class="mt-5">
              <div class="text-center">
                <Label for="name" value="Kategori Adı:" />
                <Input id="name" ref="name" type="text" v-model="form.name" class="w-1/3 hover:border-gray-500" required autocomplete="name" />
              </div>
              <div class="items-center mt-4 text-center">
                <NavLink :href="route('category.index')" class="bg-gray-400 rounded-full border-2 border-gray-900 px-7 py-1 text-gray-900" >
                  Geri Dön
                </NavLink>
                <button class="ml-4 px-10 bg-green-500 rounded-full py-1 hover:bg-green-700" :class="{ 'opacity-25': form.processing }" :disabled="form.processing" >
                  <span class="text-gray-900 ">Kaydet +</span>
                </button>
              </div>
            </form>

          </div>
        </div>
    </div>
  </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from "@/Layouts/Authenticated.vue";
import ValidationErrors from "@/Components/ValidationErrors.vue";
import Label from "@/Components/Label.vue";
import Input from "@/Components/Input.vue";
import TextArea from "@/Components/TextArea.vue";
import NavLink from "@/Components/NavLink.vue";
import Button from "@/Components/Button.vue";
import { Head } from "@inertiajs/inertia-vue3";

export default {
  components: {
    AuthenticatedLayout,
    ValidationErrors,
    Label,
    Input,
    TextArea,
    NavLink,
    Button,
    Head,
  },
  props:{
      category: Object,
  },
  data() {
    return {
        form: this.$inertia.form({
            name: this.category.name,
        }),
    };
  },
  methods: {
    submit() {
        this.form.put(this.route("category.update", this.category));
    },
  },
};

</script>
