<template>
  <div class="simple-csv-parser">
    <parse-file @fileDataReceived="fileDataReceived" ref="parseFile" lang="en"></parse-file>
  </div>
</template>

<script>
  import _ from 'lodash';
  import ParseFile from './ParseFile';
  import text from '../lang';

  export default {
    name: 'SimpleCsvParser',
    components: { ParseFile },
    props: {
      columns: {
        type: Array,
        required: true,
      },
    },
    methods: {
      parseUserColumns(columns) {
        const keys = columns.map(el => el.name);
        const data = _.unzip(columns.map(el => el.data));
        return data.map(d => _.zipObject(keys, d));
      },
      fileDataReceived(fileData) {
        this.results = [];
        const requiredColumns = this.columns.filter(column => !column.isOptional);
        if (fileData.length < requiredColumns.length) {
          const message = `${text.en.error.columnNumber}<br> ${this.columns.map(column => column.name).join('<br> ')}`;
          this.$emit('on-error', message);
          return;
        }
        this.userColumns = fileData;
        this.results = this.parseUserColumns(this.userColumns);
        this.$emit('on-load', this.results);
      },
    },
    mounted() {
    },
    data() {
      return {
        showHiddenInputs: false,
        results: [],
        userColumns: [],
      };
    },
  };
</script>
