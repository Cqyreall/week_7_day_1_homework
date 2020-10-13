<template>
  <div id="app">
    <section class="header">
      <h1 id="header"><b>ToDo's</b></h1>
    </section>
    <form v-on:submit.prevent="addNewChore">
      <label for="new-chore">Add a new item</label>
      <input type="text" id="new-item" autocomplete="off" v-model="newChore">
      <label for="priority">High</label>
      <input type="radio" id="high">
      <label for="priority">Low</label>
      <input type="radio" id="low" >
      <input type="submit" value="Save">
    </form>
    <ul>
      <li v-for="(chore, index) in chores" v-bind:class="chore.priority ? 'high' : 'low' " :key="index"> 
        <span>{{ chore.name }}</span>
        <span v-if="chore.priority === true">(High Priority)!</span>
        <span v-if="!chore.priority">(Low Priority)</span>
        <button v-if="chore.priority === true" v-on:click="changePrioritytoLow(index)">Make low priority</button>
        <button v-if="!chore.priority" v-on:click="changePrioritytoHigh(index)" class="">Make high priority</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {

      chores: [
        {name: "Shopping", priority: true},
        {name: "MOT", priority: false},
        {name: "Coding", priority: false}
      ],
      newChore: "",
    }
  
  },
  methods: {

    addNewChore: function(newChore){
      let priority = false
      if (document.querySelector('#low').checked){
        priority = false
      }
      else if (document.querySelector('#high').checked){
        priority = true
        console.log(priority)
      }
      this.chores.push({
        name: this.newChore,
        priority: priority
        }
      );
      this.newChore = ""
      document.querySelector('#high').checked = false;
      document.querySelector('#low').checked = false;
    },
    
    changePrioritytoLow: function(index){
      this.chores[index].priority = false
    },

    changePrioritytoHigh: function(index){
      this.chores[index].priority = true;
    },
  }
}
</script>

<style>
#app {
  font-family: 'Baloo Tamma 2', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
  margin: 0;
}
#header {
  margin: 0 auto;
  text-align: center;
}

.header {
  background: lightgreen;
  padding: 12px;
  margin: 0;
}



form {
  margin-top: 4%;
  text-align: center;
}

ul {
  list-style: none;
}

li{
  margin: 20px;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

li span {
  padding: 8px;
}

li.high {
  background-color: red;
  /* text-align: center; */
  border-collapse: collapse;
  width: 30%;
  border-radius: 3%;
  font-size: 16px;
  box-shadow: 5px 10px gray;
  margin-top: 5%;
  display: flex;
  justify-content: center;
  margin-left: 32%;
  color: aliceblue;
}

li.low {
  background-color: lightgreen;
  /* text-align: center; */
  border-collapse: collapse;
  width: 30%;
  border-radius: 3%;
  font-size: 16px;
  box-shadow: 5px 10px gray;
  margin-top: 5%;
  display: flex;
  align-self: center;
  margin-left: 32%;
}
</style>
