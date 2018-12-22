<template>
  <div class="card bg-success text-center col-md-6 mt-4 pt-0 px-0" id="app" v-bind:class="{'offset-3':checkWindow}">
    <div class="card-header">
    <h1 class="card-title mt-3">Word Translator</h1>
    <h5 class="card-subtitle mt-3 mb-2">Powered by Vue.js</h5>
    <h5 class="card-subtitle mt-3 mb-2">Powered by <a target="_blank" class="text-light" href="http://translate.yandex.com/">Yandex.Translate</a></h5>
    </div>
    <div class="card-body">
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
    </div>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'App',
  components:{
    TranslateForm,
    TranslateOutput
  },
  data: 
      function(){
        return{
          translatedText:''
        }
      },
  computed: {
    checkWindow:function(){
      if(window.innerWidth > 768){
        return this.bigWindow = true;
      } else {
        return this.bigWindow = false;
      }
    }
  },
  methods: {
    // text from the formSubmit value being emitted from translateform.vue
    translateText:function(text, language) {
      this.$http.get(`https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20181219T043611Z.a720d5bbefbbde16.b3f4baa4a5bb46b4e1ecb7a36305c764d097c3a4&lang=${language}&text=${text}`)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
a{
  text-decoration-line: underline;
}
</style>
