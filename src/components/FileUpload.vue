<template>
  <div class="file-upload">
    <div class="constants-upload">
      <h3>Constants</h3>
      <input type="file" id="constants-file"/>
      <p v-if="noConstantsFile">You must upload a file with your constants</p>
    </div>
    <div class="predicates-upload">
      <h3>Predicates</h3>
      <input type="file" id="predicates-file"/>
      <p v-if="noPredicatesFile">You must upload a file with your predicates</p>
    </div>
    <button v-on:click="readFiles">Generate Form</button>
  </div>
</template>

<script>
export default {
  name: "FileUpload",
  data: function() {
    return {
      noConstantsFile: false,
      noPredicatesFile: false,
    };
  },
  methods: {
    readFiles() {
      const constantsFile = document.getElementById("constants-file").files[0];
      const predicatesFile = document.getElementById("predicates-file").files[0];

      if (constantsFile === undefined){
        this.noConstantsFile = true;
      } else {
        this.noConstantsFile = false;
      }

      if (predicatesFile === undefined){
        this.noPredicatesFile = true;
      } else {
        this.noPredicatesFile = false;
      }

      if (constantsFile === undefined || predicatesFile === undefined) {
        return;
      }

      const readLines = (contents) => {
        const lines = contents
          .split("\n")
          .filter(line => line !== "");   // files may contain empty lines
        return lines;
      }

      const constants = new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = reject;
        reader.readAsText(constantsFile);
      }).then(readLines);

      const predicates = new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = reject;
        reader.readAsText(predicatesFile);
      }).then(readLines);

      Promise.all([constants, predicates]).then((values) => {
        const constants = values[0];
        const predicates = values[1];
        console.log(constants);
        console.log(predicates);
      });

    }
  }
}
</script>

<style scoped>
.file-upload {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
.constants-upload, .predicates-upload {
  padding: 1rem;
}
</style>
