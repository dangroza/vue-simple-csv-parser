<template>
  <div class="app">
    <h3>Example - Import file with required login, firstname, lastname and optional values</h3>
    <br>
    <simple-csv-parser :columns="columns" @on-load="onLoad"></simple-csv-parser>
    <br><br>
    <div class="results" v-if="results">
      <h3>Results:</h3>
      <pre>{{ JSON.stringify(results, null, 2) }}</pre>
    </div>
  </div>
</template>

<script>
  import { SimpleCsvParser } from '../src/index';

  export default {
    name: 'App',
    components: {
      SimpleCsvParser,
    },
    methods: {
      onLoad(results) {
        this.results = results;
      },
      onValidate(results) {
        this.results = results;
      },
    },
    data() {
      return {
        columns: [
          { name: 'Name', value: 'name', isOptional: true },
          { name: 'Email', value: 'email' },
        ],
        results: null,
      };
    },
  };
</script>
