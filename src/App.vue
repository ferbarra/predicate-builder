<template>
  <div id="app">
    <h1>Predicate Builder</h1>
    <!-- <FileUpload v-on:files-uploaded="createForm"/> -->
    <!-- <PredicateForm v-bind:constants="constants" v-bind:predicates="predicates"/> -->
    <component  v-bind:is="currentComponent"
                v-bind="currentComponentProperties"
                v-on:files-uploaded="showPredicateForm"
                v-on:new-predicates-and-constants="showFileUpload"></component>
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
      currentComponent: 'file-upload',
    };
  },
  computed: {
    currentComponentProperties: function () {
      if (this.currentComponent == 'predicate-form') {
        return { constants: this.constants, predicates: this.predicates };
      }
      return {};
    }
  },
  methods: {
    showPredicateForm: function(constants, predicates) {
      this.constants = constants;
      this.predicates = predicates;
      this.currentComponent = 'predicate-form';
    },
    showFileUpload: function() {
      this.currentComponent = 'file-upload';
    }
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
