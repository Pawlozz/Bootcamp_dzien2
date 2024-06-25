<template lang="html">
    <div class="mainBlog">
        <hr>
        <button @click="pobierzWpisy">Pobierz wpisy</button>
        <h2>Siema Blog!</h2>
        {{ wpisy }}
        <input v-model="nowyBlog" type="text">
        <button @click="dodajWpisy">Dodaj</button>
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
    }
}
</script>
<style lang="scss">
    hr{
        width: calc(25vw + 10%);
        color: #582785;
    }

    .mainBlog{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        gap: 2rem;
    }
</style>