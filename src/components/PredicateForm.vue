<template>
  <div class="predicate-form">
    <table>
      <tr>
        <th></th>
        <th v-for="(predicate, index) in predicates" v-bind:key="index">{{ predicate }}</th>
      </tr>
      <tr v-for="(constant, index) in constants" v-bind:key="index">
        <td>{{ constant }}</td>
        <td v-for="(_, index2) in predicates" v-bind:key="index2">
          <input type="checkbox" v-model="matrix[index][index2]"/>
        </td>
      </tr>
    </table>
    <button v-on:click="generateFile">Go</button>
    <div class="results" ref="results">
      <p v-for="(result, index) in results" v-bind:key="index">{{ result }}</p>
    </div>
    <button v-on:click="clipboard">Copy to clipboard</button>
  </div>
</template>

<script>
export default {
  name: 'PredicateForm',
  props: ['constants', 'predicates'],
  data: function () {
    return {
      results: [],
    };
  },
  computed: {
    matrix: function() {
      const matrix = [];
        for (let i = 0; i < this.constants.length; ++i) {
          const row = [];
          for (let j = 0; j < this.predicates.length; ++j) {
            row.push(false);
          }
          matrix.push(row);
        }
      return matrix;
    }
  },
  methods: {
    generateFile: function() {
      const results = [];
      for (let i = 0; i < this.predicates.length; ++i) {
        const predicate = this.predicates[i];
        for (let j = 0; j < this.constants.length; ++j) {
          if (!this.matrix[j][i]) continue;
          const constant = this.constants[j];
          results.push(`${predicate}(${constant}).`);
        }
      }
      this.results = results;
    },
    clipboard: function () {
      const results = [];
      for (let i = 0; i < this.predicates.length; ++i) {
        const predicate = this.predicates[i];
        for (let j = 0; j < this.constants.length; ++j) {
          if (!this.matrix[j][i]) continue;
          const constant = this.constants[j];
          results.push(`${predicate}(${constant}).`);
        }
      }
      const clipboardContents = results.join("\n");
      this.$copyText(clipboardContents);
    },
  }
}
</script>

<style scoped>
</style>
