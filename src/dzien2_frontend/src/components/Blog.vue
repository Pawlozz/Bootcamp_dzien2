<template lang="html">
    <div class="mainBlog">
        <h2 class="text-blue-600">Wpisy na bloga:</h2>
        <div class="w-100 flex flex-row-reverse">
            <button @click="pobierzWpisy" class="border-solid border-2 border-blue-600 rounded px-4 py-2">Refresh</button>
        </div>
        <div v-for="wpis in wpisy" class="flex flex-col gap-10 drop-shadow-x1 my-8">
            <p class="bg-blue-600 text-white py-4 px-4 rounded">{{ wpis }}</p>
        </div>
        <label for="post">Dodaj post</label>
        <input v-model="nowyBlog" name="post" id="post" type="text" class="border-solid border-2 border-blue-600 rounded mx-4">
        <button @click="dodajWpisy" class="border-solid border-2 border-blue-600 rounded px-4 py-0">Dodaj</button>
    </div>
</template>
<script>
import { dzien2_backend } from 'declarations/dzien2_backend/index';

export default {
    data(){
        return{
            wpisy:  [],
            nowyBlog: ""
        }
    },
    methods: {
        async dodajWpisy(){
            await dzien2_backend.dodaj_wpis(this.nowyBlog);
        },
        async pobierzWpisy(){
            this.wpisy = await dzien2_backend.odczytaj_wpisy();
        }
    },
    async mounted(){
        this.pobierzWpisy()
    }
}
</script>