<template>
  <div id="app">
    <h1>Predicate Builder</h1>
    <FileUpload v-on:files-uploaded="createForm"/>
    <PredicateForm v-bind:constants="constants" v-bind:predicates="predicates"/>
  </div>
</template>

<script>
import FileUpload from './components/FileUpload.vue'
import PredicateForm from './components/PredicateForm.vue'

export default {
  name: 'App',
  components: {
    FileUpload,
    PredicateForm,
  },
  data: function() {
    return {
      constants: [],
      predicates: [],
    };
  },
  methods: {
    createForm: function(constants, predicates) {
      this.constants = constants;
      this.predicates = predicates;
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  text-align: center;
}
</style>
