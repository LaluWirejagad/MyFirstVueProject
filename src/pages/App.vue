<template>
  <main-layout>
    <form id="search">
        Search <input name="query" v-model="searchQuery" />
      </form>
    <TableData :heroes='gridData' :columns= 'gridColumns' :filterKey='searchQuery'/>
  </main-layout>
</template>

<script>
import MainLayout from '../layouts/Main.vue'
import TableData from '../components/TableData.vue'

export default {
  name: 'App',
  components: {
    MainLayout,
    TableData
  },
  async created(){
    try {
      const requestOptions = {
        method: "GET",
        headers: { "Content-Type": "application/json" },
      };
      const response = await fetch("https://reqres.in/api/users?page=1", requestOptions);
      const data = await response.json();
      console.log(data)
      this.gridData = data.data
    } catch (error) {
      console.error('There was an error!', error);
    }
  },
  data() {
    return {
      searchQuery: '',
      gridColumns: ['id','first_name','last_name', 'email'],
      gridData: []
    }
  },
}
</script>


