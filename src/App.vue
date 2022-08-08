<script>
import countries from './components/countries.vue';
export default{
    components: {
        countries,
    },
    data(){
        return {
            message: 'Traduire le texe',
            countries:countries.data().languages,
        }
    },
    methods: {
        translateFunction(){
            let api = `https://api.mymemory.translated.net/get?q=${text}&langpair=${translateFrom}|${translateTo}`;
        }
    },
    mounted() {
        
    },
}
</script>

<template>
    <div class="container">
        <div class="wrapper">
            <div class="text-input">
                <textarea spellcheck="false" v-model="translateFrom" class="from-text" placeholder="Entrer le texte"></textarea>
                <textarea spellcheck="false" v-model="translateTo" readonly disabled class="to-text" placeholder="Translation"></textarea>
            </div>
            <ul class="controls">
                <li class="row from">
                    <div class="icons">
                    <i id="from" class="fas fa-volume-up"></i>
                    <i id="from" class="fas fa-copy"></i>
                    </div>
                    <select >
                        <option  v-for="(index, lang) in countries" :key="index">{{countries[lang]}}</option>
                    </select>
                </li>
                <li class="exchange"><i class="fas fa-exchange-alt"></i></li>
                <li class="row to">
                    <select>
                        <option  v-for="(index, lang) in countries" :key="index">{{countries[lang]}}</option>
                    </select>
                    <div class="icons">
                    <i id="to" class="fas fa-volume-up"></i>
                    <i id="to" class="fas fa-copy"></i>
                    </div>
                </li>
            </ul>
        </div>
        <button @click="sayHello">{{message}}</button>
    </div>
</template>

<style scoped>
    @import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css");
</style>
