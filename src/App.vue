<script>
export default{
    data(){
        return {
            btnMessage: 'Traduire le texte',
            translateFrom: 'en-GB',
            translateTo: 'fr-FR',
            translateText: '',
            selected: '',
            Logique:"",
            textFrom:'',
            textTo:'',
            languages: {
                "am-ET": "Amharic",
                "ar-SA": "Arabic",
                "be-BY": "Bielarus",
                "bem-ZM": "Bemba",
                "bi-VU": "Bislama",
                "bjs-BB": "Bajan",
                "bn-IN": "Bengali",
                "bo-CN": "Tibetan",
                "br-FR": "Breton",
                "bs-BA": "Bosnian",
                "ca-ES": "Catalan",
                "cop-EG": "Coptic",
                "cs-CZ": "Czech",
                "cy-GB": "Welsh",
                "da-DK": "Danish",
                "dz-BT": "Dzongkha",
                "de-DE": "German",
                "dv-MV": "Maldivian",
                "el-GR": "Greek",
                "en-GB": "English",
                "es-ES": "Spanish",
                "et-EE": "Estonian",
                "eu-ES": "Basque",
                "fa-IR": "Persian",
                "fi-FI": "Finnish",
                "fn-FNG": "Fanagalo",
                "fo-FO": "Faroese",
                "fr-FR": "French",
                "gl-ES": "Galician",
                "gu-IN": "Gujarati",
                "ha-NE": "Hausa",
                "he-IL": "Hebrew",
                "hi-IN": "Hindi",
                "hr-HR": "Croatian",
                "hu-HU": "Hungarian",
                "id-ID": "Indonesian",
                "is-IS": "Icelandic",
                "it-IT": "Italian",
                "ja-JP": "Japanese",
                "kk-KZ": "Kazakh",
                "km-KM": "Khmer",
                "kn-IN": "Kannada",
                "ko-KR": "Korean",
                "ku-TR": "Kurdish",
                "ky-KG": "Kyrgyz",
                "la-VA": "Latin",
                "lo-LA": "Lao",
                "lv-LV": "Latvian",
                "men-SL": "Mende",
                "mg-MG": "Malagasy",
                "mi-NZ": "Maori",
                "ms-MY": "Malay",
                "mt-MT": "Maltese",
                "my-MM": "Burmese",
                "ne-NP": "Nepali",
                "niu-NU": "Niuean",
                "nl-NL": "Dutch",
                "no-NO": "Norwegian",
                "ny-MW": "Nyanja",
                "ur-PK": "Pakistani",
                "pau-PW": "Palauan",
                "pa-IN": "Panjabi",
                "ps-PK": "Pashto",
                "pis-SB": "Pijin",
                "pl-PL": "Polish",
                "pt-PT": "Portuguese",
                "rn-BI": "Kirundi",
                "ro-RO": "Romanian",
                "ru-RU": "Russian",
                "sg-CF": "Sango",
                "si-LK": "Sinhala",
                "sk-SK": "Slovak",
                "sm-WS": "Samoan",
                "sn-ZW": "Shona",
                "so-SO": "Somali",
                "sq-AL": "Albanian",
                "sr-RS": "Serbian",
                "sv-SE": "Swedish",
                "sw-SZ": "Swahili",
                "ta-LK": "Tamil",
                "te-IN": "Telugu",
                "tet-TL": "Tetum",
                "tg-TJ": "Tajik",
                "th-TH": "Thai",
                "ti-TI": "Tigrinya",
                "tk-TM": "Turkmen",
                "tl-PH": "Tagalog",
                "tn-BW": "Tswana",
                "to-TO": "Tongan",
                "tr-TR": "Turkish",
                "uk-UA": "Ukrainian",
                "uz-UZ": "Uzbek",
                "vi-VN": "Vietnamese",
                "wo-SN": "Wolof",
                "xh-ZA": "Xhosa",
                "yi-YD": "Yiddish",
                "zu-ZA": "Zulu",
                },
        }
    },
    methods: {
        translateTextFunc(){
            // console.log(this.languages);
            let textTrime = this.textFrom.trim();
            console.log(textTrime);
            
            // this.selected = id == 0 ? country_code == "en-GB" ? "selected" : "" : country_code == "fr-FR" ? "selected" : "";
            let apiUrl = `https://api.mymemory.translated.net/get?q=${textTrime}&langpair=${this.translateFrom}|${this.translateTo}`;
            fetch(apiUrl).then(res => res.json()).then(data => {
                console.log(data);
                toText.value = data.responseData.translatedText;
                data.matches.forEach(data => {
                    if(data.id === 0) {
                        // toText.value = data.translation;
                        console.log(data.translation);
                    }
                })
                // toText.setAttribute("placeholder", "Translation");
            }).catch(error => {
                    console.log("Hey quelques choses s'est très mal passée !" + error);
            }) ;
        },
        translateSound(){
            console.log("translateSound");
        },
        translateFromFunc(){
            
        },
        copyText: function(){
            console.log('Hey we are copying');
        },
        exchangeFunc: function(){
            console.log("hey, we are here");
        }

    },
    computed: {
        translateFromOptions: function(){
            return this.languages;
        },
        translateToOptions: function(){
            return this.languages;
        }
    },
    // props:{
    //     id: String,
    // }
}
</script>

<template>
    <div class="container">
        <div class="wrapper">
            <div class="text-input">
                <textarea 
                    spellcheck="false" 
                    v-model="textFrom" 
                    class="from-text" 
                    placeholder="Entrer le texte"
                >
                </textarea>
                <textarea 
                    spellcheck="false" 
                    v-model="textTo" 
                    readonly 
                    disabled 
                    class="to-text" 
                    placeholder="Translation"
                >
                </textarea>
            </div>
            <ul class="controls">
                <li class="row from">
                    <div class="icons">
                    <i 
                        id="from" 
                        @click="translateSound()" 
                        class="fas fa-volume-up"
                    >
                    </i>
                    <i 
                        @click="copyText()"
                        id="from" 
                        class="fas 
                        fa-copy"
                    >
                    </i>
                    </div>
                    <select v-model="translateFrom" >
                        <option  
                            v-for="(index, lang) in languages" 
                            :key="index"
                            :value="lang"
                            :selected="lang == 'en-GB' ? true : false" 
                        >
                            {{ languages[lang] }}
                        </option>
                    </select>
                </li>
                <li @click="exchangeFunc" class="exchange"><i class="fas fa-exchange-alt"></i></li>
                <li class="row to">
                    <select v-model="translateTo" >
                        <option  
                            v-for="(index, lang) in languages"
                            :key="index"
                            :value="lang"
                            :selected="lang == 'fr-FR' ? true : false" 
                        >
                            {{ languages[lang] }}
                        </option>
                    </select>
                    <div class="icons">
                    <i 
                        @click="translateSound()"
                        id="to" 
                        class="fas fa-volume-up"
                    >
                    </i>
                    <i 
                        @click="copyText()"
                        id="to" 
                        class="fas fa-copy"
                    >
                    </i>
                    </div>
                </li>
            </ul>
        </div>
        <button @click="translateTextFunc">{{ btnMessage }}</button>
    </div>
</template>

<style scoped>
    @import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css");
</style>
