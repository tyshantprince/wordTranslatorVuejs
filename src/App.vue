<template>
  <div class="text-center" id="app">

    <h1>Word Translator</h1>
    <h5>Powered By Vue.js</h5>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'app',
  components:{
    TranslateForm,
    TranslateOutput
  },
  data: function() {
    return{
      translatedText: ''
    }
  },
  methods: {
    translateText: function(text, language) {
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170414T164914Z.4ccc3b72f012e8a3.9d3ab6dcc2168c903225903ffebae07751c1a9e2&lang=' + language + '&text=' +text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
body {
  background: #fefefe;

}
</style>
