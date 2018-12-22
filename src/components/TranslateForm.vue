<template>
  <div id="translateForm">
    <form class="" v-on:submit="formSubmit">
      <div class="form-group row mt-2">
      <input class="form-control col-md-5 mx-auto" type="text" v-model="textToTranslate" placeholder="Enter a word">
      <select class="form-control col-md-4 mx-auto" v-model="language">
        <option value="es">Spanish</option>
        <option value="ko">Korean</option>
        <option value="fr">French</option>
        <option value="pt">Portuguese</option>
        <option value="ru">Russian</option>
        <option value="sv">Swedish</option>
        <option value="en">English</option>
      </select>
      <input class="btn btn-dark text-light mx-auto" type="submit" value="Translate">
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'translateForm',
  data(){
    return {
      textToTranslate:'',
      language:''
    }
  },
  // Runs only when the elements included in these methods are created
  created(){
    this.language = 'es';
  },
  methods: {
    formSubmit(e){
      // 'Emits' the textToTranslate value to the formSubmit attribute(in App.vue)
      this.$emit('formSubmit', this.textToTranslate, this.language)
      e.preventDefault();
    }
  }
}
</script>

<style>

</style>