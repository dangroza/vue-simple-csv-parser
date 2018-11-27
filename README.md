# Simple Vue XLS/CSV parser

## Description

This npm package is based on https://github.com/victorboissiere/vue-xls-csv-parser
The objective for this library was to create a simplified component that returns the parsed file as an array of objects pe row
## Requirements

You will need Bootstrap 3.x. It has not been tested yet with Boostrap 4.

## Components

### XlsCsvParser, SimpleCsvParser

#### Example usage
```html
<template>
  <div class="app">
    <h3>Example - Import file with required login, firstname, lastname and optional values</h3>
    <br>
    <simple-csv-parser :columns="columns" @on-load="onLoad" @on-error="onError"></simple-csv-parser>
    <br><br>
    <div class="results" v-if="results">
      <h3>Results:</h3>
      <pre>{{ JSON.stringify(results, null, 2) }}</pre>
    </div>
  </div>
</template>

<script>
  import { SimpleCsvParser } from 'vue-xls-csv-parser';
  export default {
    name: 'App',
    components: {
      SimpleCsvParser,
    },
    methods: {
      onLoad(results) {
        this.results = results;
      },
      onError(message) {
        // handle error;
      },
    },
    data() {
      return {
        columns: [
          { name: 'Student login', value: 'login' },
          { name: 'Student firstname', value: 'firstname' },
          { name: 'Student lastname', value: 'lastname' },
          { name: 'Other', value: 'other', isOptional: true },
        ],
        results: null,
        help: 'Necessary columns are: login, firstname and lastname',
      };
    },
  };
</script>
```
## Build Setup

``` bash
# install dependencies
yarn intall

# serve with hot reload at localhost:8080
yarn start

# build for a release
yarn bundle:dist
```
