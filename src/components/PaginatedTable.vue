<template>
  <loadable-area :loading="true">
    <div class="pagination-header">
      <div>
        <div>Show</div>
        <div>
          <select>
            <option value="10">10</option>
          </select>
        </div>
        <div>entries</div>
      </div>
    </div>
    <table class="table" cellspacing="0">
      <thead class="table-head">
        <tr>
          <th v-for="(col, index) in colNames" :key="index">
            {{ col }}
          </th>
          <th v-if="edit"></th>
          <th v-if="del"></th>
          <th v-if="view"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, index) in content" :key="index">
          <template v-if="index < size">
            <td v-for="(cell, index) in row" :key="index">
              {{ cell }}
            </td>
          </template>
          <td v-if="edit"><button type="button" style="background: #3f51b5;" @click="editRecord(row)">Edit</button></td>
          <td v-if="del"><button type="button" style="background: #ba000d" @click="delRecord(row)">Delete</button></td>
          <td v-if="view"><button type="button" style="background: #087f23" @click="viewRecord(row)">View</button></td>
        </tr>
      </tbody>
    </table>
    <div class="pagination-footer">
      <div>
        <div>Showing {{ page * size + 1 }} to {{ page * size + size }} of entries {{ max }}</div>
      </div>
      <div>
        <div>
          <button type="button">
            Previous
          </button>
        </div>
        <div>
          <select>
            <option v-for="i in pages()" :key="i" v-bind:value="i - 1">{{ i }}</option>
          </select>
        </div>
        <div>
          <button type="button">
            Next
          </button>
        </div>
      </div>
    </div>
  </loadable-area>
</template>

<script>
import LoadableArea from './LoadableArea.vue';

export default {
  name: "PaginatedTable",
    components: {
        LoadableArea
  },
  props: {
    colNames: Array,
    edit: {
      type: Boolean,
      required: false,
      default: false,
    },
    del: {
      type: Boolean,
      required: false,
      default: false,
    },
    view: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  data() {
    return {
      content: [
        { id: 1, fName: "Chris", lName: "Brighton", address: "38 Beresford Close, SP10 2HN" },
        { id: 2, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 3, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 4, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 5, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 6, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 7, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 8, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 9, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
        { id: 10, fName: "Jason", lName: "Ripley", address: "4 Amber Drive, SP11 3RW" },
      ],
      max: 101,
      size: 10,
      sizes: [10, 25, 50],
      page: 0,
      pages() {
        return Math.ceil(this.max / this.size);
      },
    };
  },
  methods: {
    editRecord(record) {
      this.$emit("on-edit", record);
    },
    delRecord(record) {
      this.$emit("on-delete", record);
    },
    viewRecord(record) {
      this.$emit("on-view", record);
    },
    toggleLoad(loading) {
      this.$emit("loading", loading);
    },
  },
};
</script>

<style scoped>
.pagination-header,
table,
.pagination-footer {
  width: 90%;
  margin: 0 5%;
}
table {
  margin: 4px 5%;
}
.pagination-header,
.pagination-footer,
.pagination-header > div,
.pagination-footer > div {
  display: flex;
  flex-direction: row;
  height: 40px;
  align-items: center;
}
.pagination-header > div > div {
  margin: 0 3px;
}

.table > thead > tr > th {
  background: #333338;
  padding: 4px 0;
}

.table > tbody > tr > td {
  padding: 4px 0;
}

.table > tbody > tr:nth-child(even) > td {
  background: #555;
  border-top: 1px solid #666;
  border-bottom: 1px solid #666;
}
.table > tbody > tr:nth-child(odd) > td {
  background: #444;
}

.pagination-footer {
  justify-content: space-between;
}
.pagination-footer > div:last-child > div {
  margin: 0 4px;
}
</style>
