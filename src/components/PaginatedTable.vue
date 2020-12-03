<template>
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
        <table class="table">
            <thead class="table-head">
                <tr>
                    <th v-for="(col, index) in colNames" :key="index">
                        {{col}}
                    </th>
                    <th v-if="edit"></th>
                    <th v-if="del"></th>
                    <th v-if="view"></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(row, index) in content" :key="index">
                    <td v-for="(cell, index) in row" :key="index">
                        {{cell}}
                    </td>
                    <td v-if="edit"><button type="button" @click="editRecord(row)">Edit</button></td>
                    <td v-if="del"><button type="button" @click="delRecord(row)">Delete</button></td>
                    <td v-if="view"><button type="button" @click="viewRecord(row)">View</button></td>
                </tr>
            </tbody>
        </table>
        <div class="pagination-footer">
            <div>
                <div>
                    Showing   to   of   entries
                </div>
            </div>
            <div>
                <div>
                    <button type="button">
                        Previous
                    </button>
                </div>
                <div>
                    <select>
                        <option value="0">0</option>
                    </select>
                </div>
                <div>
                    <button type="button">
                        Next
                    </button>
                </div>
            </div>
        </div>
</template>

<script>

export default {
    name : 'PaginatedTable',
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
            content : [
                {id: 1, fName:'Chris', lName:'Brighton', address:'38 Beresford Close, SP10 2HN'},
                {id: 2, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 3, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 4, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 5, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 6, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 7, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 8, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 9, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
                {id: 10, fName:'Jason', lName:'Ripley', address:'4 Amber Drive, SP11 3RW'},
            ],
            max : 101,
            size : 10,
            page : 0,
            pages() {
                return
            },
        }
    },
    methods: {
        editRecord(record) {
            this.$emit('on-edit', record);
        },
        delRecord(record) {
            this.$emit('on-delete', record);
        },
        viewRecord(record) {
            this.$emit('on-view', record);
        },
        toggleLoad(loading) {
            this.$emit('loading', loading);
        }
    },

}
</script>

<style scoped>
    .pagination-header, table, .pagination-footer {
        width: 90%;
        margin: 0 5%;
    }
    .pagination-header, .pagination-footer, .pagination-header > div, .pagination-footer > div {
        display: flex;
        flex-direction: row;
        height: 40px;
        align-items: center;
    }
    .pagination-header > div > div {
        margin: 0 3px;
    }
    .pagination-footer {
        justify-content: space-between;
    }
    .pagination-footer > div:last-child > div {
        margin: 0 4px;
    }
</style>