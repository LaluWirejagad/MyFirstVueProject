<template>
  <main-layout>
    <form id="search">
      Search <input name="query" v-model="searchQuery" />
    </form>
    <center>
    <table>
      <thead>
        <tr>
          <th>
            No.
          </th>
          <th>
            Operation
          </th>
          <th>
            Saved Time
          </th>
          <th>
            Action
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(entry,i) in filteredDatas" v-bind:key="entry">
          <td>
            {{ i+1}}
          </td>
          <td>
            {{ entry.value }}
          </td>
          <td>
            {{ entry.savedTime }}
          </td>
          <td>
            <button @click="deleteData(i)">DELETE</button>
          </td>
        </tr>
      </tbody>
    </table>
  </center>
  </main-layout>
</template>

<script>
import MainLayout from '../layouts/Main.vue'

export default {
  components: {
    MainLayout,
  },
  async created(){
    if(localStorage.getItem('saveOperations')) {
      try {
        this.gridData = JSON.parse(localStorage.getItem('saveOperations'));
      } catch(e) {
        localStorage.removeItem('saveOperations');
      }
    }
  },
  computed: {
    filteredDatas() {
      const filterKey = this.searchQuery && this.searchQuery.toLowerCase()
      let datas = this.gridData
      if (filterKey) {
        datas = datas.filter(function(row) {
          return Object.keys(row).some(function(key) {
            return (
              String(row[key])
                .toLowerCase()
                .indexOf(filterKey) > -1
            )
          })
        })
      }
      return datas
    }
  },
  data() {
    return {
      selected:0,
      searchQuery: '',
      gridData: []
    }
  },
  methods:{
    deleteData(i){
      try {
        this.gridData.splice(i, 1);
        const parsed = JSON.stringify(this.gridData);
        localStorage.setItem('saveOperations', parsed);
      } catch(e) {
        localStorage.removeItem('saveOperations');
      }
    }
  }
}
</script>

<style scoped>

body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}

table {
  margin: 20px;
  border: 2px solid #42b983;
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

</style>
