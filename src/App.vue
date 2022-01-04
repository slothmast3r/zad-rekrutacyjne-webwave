<template>
  <div id="app">
    <h1>Losowe ustawianie elementów na tablicy</h1>
    <transition-group name="flip-list" tag="div" class="table-wrapper">
      <tab-element
          v-for="el in arr"
          :key="el.id"
          :columns-count="columnsCount"
          :is-active="el.isActive"
          :title="el.title"
          @component-clicked="selectElement(el)"
      />
    </transition-group>
    <button @click="shuffleArr">Wymieszaj</button>
    <input v-model="inputElement.title">
  </div>
  <div class="footer">Oskar Straszyński</div>
</template>

<script>


import TabElement from "@/components/TabElement";
import { shuffle } from "../script/algorithms";

export default {
  name: 'App',
  components: {
    TabElement
  },
  data(){
    return {
      arr: [],
      elementsCount: 6,
      columnsCount: 3,
      inputElement: {title: ''},
    }
  },
  created() {
    this.createData()
  },
  methods:{
    createData(){
      this.arr =[...Array(6)].map((item, index) => ({title:'Tytuł' + index, id:  index, isActive: false}))
    },
    shuffleArr(){
      this.arr = shuffle(this.arr);
    },
    selectElement(el){
      this.inputElement.isActive = false
      this.inputElement = el
      this.inputElement.isActive = true
    },
  }
}
</script>

<style lang="scss">


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.table-wrapper{
  display: flex;
  list-style-type: none;
  flex-wrap: wrap;
  margin-bottom: 40px;
}


.flip-list-move {
  transition: transform 0.8s ease;
}
button{
  margin: 10px;
}
.footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  padding: 30px;
  text-align: left;
  border-top: 1px solid black;
  background: white;
}
</style>
