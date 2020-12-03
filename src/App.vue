<template>
  <screenlet :loading="loading.table">
    <paginated-table
      :colNames="['Id', 'First Name', 'Last Name', 'Address']"
      :edit="true"
      :del="true"
      @on-edit="editRecord"
      @on-delete="deleteRecord"
      @loading="(loading) => load('table', loading)"
    />
  </screenlet>
  <screenlet> </screenlet>
</template>

<script>
import PaginatedTable from "./components/PaginatedTable.vue";
import Screenlet from "./components/Screenlet.vue";

export default {
  name: "App",
  components: {
    PaginatedTable,
    Screenlet,
  },
  data() {
    return {
      loading: {
        table: false,
      },
    };
  },
  methods: {
    editRecord(record) {
      console.log("EDIT RECORD", record);
    },
    deleteRecord(record) {
      console.log("DELETE RECORD", record);
    },
    load(name, loading) {
      this.loading[name] = loading;
    },
  },
};
</script>

<style>
* {
  outline: none;
  padding: 0;
  margin: 0;
  font-size: 1em;
}
*:hover,
*:active {
  outline: none;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  text-align: center;
  flex-direction: column;
}
button {
  color: white;
  background: orangered;
  border: none;
  padding: 3px 6px;
  box-shadow: 2px 2px 2px 0px rgba(0, 0, 0, 0.5);
  transition: all linear 0.2s;
  font-size: 1.03em;
}
button:hover {
  box-shadow: 4px 4px 4px 0px rgba(0, 0, 0, 0.4);
  cursor: pointer;
}
</style>
