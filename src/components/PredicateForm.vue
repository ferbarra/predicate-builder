<template>
  <div class="predicate-form">
    <table>
      <tr>
        <th></th>
        <th v-for="(predicate, index) in predicates" v-bind:key="index">{{ predicate }}</th>
      </tr>
      <tr v-for="(constant, index) in constants" v-bind:key="index">
        <td class="constant">{{ constant }}</td>
        <td v-for="(_, index2) in predicates" v-bind:key="index2">
          <input type="checkbox" v-model="matrix[index][index2]"/>
        </td>
      </tr>
    </table>
    <button v-on:click="generateFile">Compute predicates</button>
    <div class="facts">
      <div class="header">
        <button v-on:click="clipboard">Copy to clipboard</button>
      </div>
      <div class="body">
        <p v-for="(result, index) in results" v-bind:key="index">{{ result }}</p>
      </div>
    </div>
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

<style lang="scss" scoped>
.predicate-form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-top: 1rem;
  padding-bottom: 1.5rem;
}

.constant {
  background-color: lightgray;
}
table {
  border-collapse: collapse;
}
th, td {
  border: 1px solid gray;
}

th {
  padding: 0.5rem 1rem; 
}

td {
  text-align: center;
}

button {
  margin: 1rem;
}

.facts {
  min-width: 30%;
  border: 1px solid;
  border-color: #ddd;
  border-radius: 5px;

  .header {
    text-align: right;
    background-color: #f5f5f5;
    border-bottom: 1px solid;
    border-color: #ddd;
    button {
      margin: 5px;
    }
  }
  .body {
    padding: 1rem;
    border-radius: 0 0 5px 5px;
    p {
      margin: 0.4rem;
      font-size: 1.2rem;
    }
  }
}
</style>
