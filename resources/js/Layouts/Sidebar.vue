
<template>
    <div class="w-64 absolute bg-sky-800 shadow h-full left-0 mt-20">
                            <div>
                                Kategoriler
                            </div>
                            <div v-for="category in categories" :key="category.id">
                                {{ category.name }}
                            </div>
                        </div>
</template>

