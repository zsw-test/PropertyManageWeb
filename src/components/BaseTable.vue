<template>
  <table class="table tablesorter" :class="tableClass">
    <thead :class="theadClasses">
    <tr>
      <slot name="columns">
        <th v-for="column in columns" :key="column">{{column}}</th>
      </slot>
    </tr>
    </thead>
    <tbody :class="tbodyClasses">
    <tr v-for="(item, index) in data" :key="index">
      <slot :row="item">
        <td v-for="(column, index) in columns"
            :key="index"
            v-if="hasValue(item, column)">
          {{itemValue(item, column)}}
        </td>
        <td class="td-actions text-right">
            <base-button  v-on:click="say('hi')" type="info" size="sm" icon >
              <i class="tim-icons icon-single-02"></i>
            </base-button>
            <base-button v-on:click="say('hi')" type="success" size="sm" icon>
              <i class="tim-icons icon-settings"></i>
            </base-button>
            <base-button  v-on:click="say('hi')" type="danger" size="sm" icon>
              <i class="tim-icons icon-simple-remove"></i>
            </base-button>
          </td>
      </slot>
    </tr>
    </tbody>
  </table>
</template>
<script>
  export default {
    name: 'base-table',
    props: {
      columns: {
        type: Array,
        default: () => [],
        description: "Table columns"
      },
      data: {
        type: Array,
        default: () => [],
        description: "Table data"
      },
      type: {
        type: String, // striped | hover
        default: "",
        description: "Whether table is striped or hover type"
      },
      theadClasses: {
        type: String,
        default: '',
        description: "<thead> css classes"
      },
      tbodyClasses: {
        type: String,
        default: '',
        description: "<tbody> css classes"
      }
    },
    computed: {
      tableClass() {
        return this.type && `table-${this.type}`;
      }
    },
    methods: {
      hasValue(item, column) {
        return item[column] !== "undefined";
      },
      itemValue(item, column) {
        return item[column];
      },
      say: function (message) {
      alert(message)
    }

    }
  };
</script>
<style>
</style>
