<template>
  <main-layout>
    <center>
      <tr>
        <td colspan="2">
            <p>First Number</p><input type="number" v-model="firstNum" />
        </td>
        <td colspan="2">
          <p>Second Number</p><input type="number" v-model="secondNum" />
        </td>
      </tr>
      <tr>
        <td>
              <button @click="add()">Addition</button>
        </td>
        <td>
              <button @click="minus()">Substraction</button>
        </td>
        <td>
              <button @click="devide()">Division</button>
        </td>
        <td>
              <button @click="modulo()">Mod</button>
        </td>
      </tr>
      <tr>
        <td colspan="4">
              <h1>{{result}}</h1>
        </td>
      </tr>
      <tr v-if="result || result === 0">
        <td colspan="4">
              <button @click="save()">Save Operation To Local</button>
        </td>
      </tr>
    </center>
  </main-layout>
</template>

<script>
import MainLayout from '../layouts/Main.vue'

export default {
  components: {
    MainLayout
  },
  data() {
    return {
      firstNum:1,
      secondNum: 1,
      result:"",
      operand:"",
    }
  },
  methods:{
    add(){
     this.result =  this.firstNum+this.secondNum
     this.operand = " + "
    },
    minus(){
     this.result =  this.firstNum-this.secondNum
     this.operand = " - "
    },
    devide(){
     this.result =  this.firstNum/this.secondNum
     this.operand = " / "
    },
    modulo(){
     this.result =  this.firstNum%this.secondNum
     this.operand = " % "
    },
    save(){
      var saveString = this.firstNum+this.operand+this.secondNum+" = "+this.result
      var currentdate = new Date(); 
      var saveDate = currentdate.getDate() + "/"
                + (currentdate.getMonth()+1)  + "/" 
                + currentdate.getFullYear() + " @ "  
                + currentdate.getHours() + ":"  
                + currentdate.getMinutes() + ":" 
                + currentdate.getSeconds();
      if(localStorage.getItem('saveOperations')) {
        try {
          var list = []
          list = JSON.parse(localStorage.getItem('saveOperations'));
          list.push({value:saveString,savedTime:saveDate})
          const parsed = JSON.stringify(list);
          localStorage.setItem('saveOperations', parsed);
        } catch(e) {
          localStorage.removeItem('saveOperations');
        }
      }else{
          try {
          var newlist = []
          newlist.push({value:saveString,savedTime:saveDate})
          const parsed = JSON.stringify(newlist);
          localStorage.setItem('saveOperations', parsed);
        } catch(e) {
          localStorage.removeItem('saveOperations');
        }
      }
    }
  }
}
</script>


<style scoped>
td {
  min-width: 120px;
  padding: 10px 20px;
}
</style>