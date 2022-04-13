


<template>
  <Head title="Applications" />
  <AuthenticatedLayout>

    <div class="py-12">
        <div class="overflow-hidden">
          <div class="p-6">
            <ValidationErrors class="mb-4" />

            <div v-if="$page.props.flash.message" class="mb-4 font-medium text-sm text-green-600">
              {{ $page.props.flash.message }}
            </div>
            <div v-if="$page.props.flash.error" class="mb-4 font-medium text-sm text-green-600">
              {{ $page.props.flash.error }}
            </div>

            <div class="text-center text-3xl font-serif font-medium tracking-wider">
                <h1 class="text-gray-600">{{ post.title }} Post Edit</h1>
            </div>

            <form @submit.prevent="submit">
              <div class="text-center mt-3">
                <Label for="title" value="Başlık:" />
                <Input id="title" ref="title" type="text" v-model="form.title" class="w-1/4 hover:border-gray-500" required autocomplete="title" />
              </div>

                <div class="mx-auto w-1/4">
                    <Label for="resim">Resim:</Label>
                    <label class="file-select">
                        <div class="select-button cursor-pointer hover:bg-green-800 text-gray-900">
                        <span v-if="value">Selected File: {{value.name}}</span>
                        <span v-else>Ekle +</span>
                        </div>
                        <input type="file" @change="handleFileChange"/>
                    </label>
                </div>

                <div class="mx-auto text-center items-center mt-3">
                    <Label for="content" value="İçerik:" />
                    <TextArea id="content" ref="content" v-model="form.content" class=" hover:border-gray-500" required autocomplete="content" />
                </div>

                <div class="mx-auto text-center items-center">
                    <select v-if="categories" id="categories" ref="categories" v-model="form.category_id" required class="border border-gray-300 focus:border-gray-400 focus:ring focus:ring-teal-600 focus:ring-opacity-30 rounded-md shadow-sm p-3 pr-7">
                        <option value="">Choose Category</option>
                        <option v-for="cat in categories" :key="cat.id" :value="cat.id" :selected="cat.id == category.id">{{ cat.name }}</option>
                    </select>
                </div>


              <div class="items-center mt-4 text-center">
                <Button class="ml-4 px-7 bg-green-600 rounded-full hover:bg-green-700" :class="{ 'opacity-25': form.processing }" :disabled="form.processing" >
                  <span class="text-gray-900">Kaydet +</span>
                </Button>
                <button @click="delPost(post)" type="button" class="">
                            <!-- top -->
                            <div class="flex flex-row justify-between items-center rounded-full bg-red-600 px-5 py-1 text-white">
                                <span>Sil</span>
                            </div>
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
    name:'imageUpload',
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
  props: {
      post: Object,
      value: File
  },
  data() {
    return {
        form: this.$inertia.form({
            category_id: this.post.category_id,
            title: this.post.title,
            img: this.post.img,
            content: this.post.content,
        }),
    };
  },
  methods: {
    handleFileChange(e) {
      this.form.img = e.target.files[0];
    },
    delPost(post) {
        if (confirm('Are you sure you want to delete this Post?')) {
            this.$inertia.delete(this.route("post.destroy", post));
        }
    },
    submit() {
        this.form.post(this.route("post.store"));
    },
  },
};

</script>

<style scoped>
.file-select > .select-button {
  padding: 1rem;

  color: white;
  background-color: #2EA169;

  border-radius: .3rem;

  text-align: center;
  font-weight: bold;
}

.file-select > input[type="file"] {
  display: none;
}
</style>
