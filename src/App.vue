<template>
  <div id="app">
    <h1>Losowe ustawianie elementów na tablicy</h1>
    <transition-group name="flip-list" tag="div" class="table-wrapper" v-click-outside="deselectElement">
      <tab-element
          v-for="el in arrList"
          :key="el.id"
          :columns-count="Number(columnsCount)"
          :is-active="el.isActive"
          :title="el.title"
          @component-clicked="selectElement(el)"
      />
    </transition-group>
    <div>
      <button @click="shuffleArr">Wymieszaj</button>
    </div>
    <div>
    <input v-model="inputElement.title" :placeholder="'Zmień tytuł'">
    </div>
    <div>
      <div>Liczba Elementów</div>
      <input type="range" :min="minAmountOfElements" :max="maxAmountOfElements" v-model="elementsCount">
    </div>
    <div>
      <div>Liczba Kolumn</div>
      <input type="range" :min="minAmountOfRows" :max="maxAmountOfRows" v-model="columnsCount">
    </div>
  </div>
  <div class="footer">Oskar Straszyński</div>
</template>

<script>


import TabElement from "@/components/TabElement";
import { shuffle } from "../script/algorithms";
import vClickOutside from "v-click-outside";

export default {
  name: 'App',
  directives: {
    clickOutside: vClickOutside.directive
  },
  components: {
    TabElement
  },
  data(){
    return {
      arr: [],
      elementsCount: 6,
      columnsCount: 3,
      inputElement: {title: ''},
      minAmountOfElements: 2,
      maxAmountOfElements: 40,
      minAmountOfRows: 2,
      maxAmountOfRows: 10,
    }
  },
  computed:{
    arrList(){
      return this.arr.filter((x,index)=> index < this.elementsCount)
    }
  },
  created() {
    this.createData()
  },
  methods:{
    createData(){
      this.arr = [...Array(this.maxAmountOfElements)].map((item, index) => ({title:'Tytuł ' + index, id:  index, isActive: false}))
    },
    shuffleArr(){
      this.arr = shuffle(this.arr);
    },
    selectElement(el){
      this.inputElement.isActive = false
      this.inputElement = el
      this.inputElement.isActive = true
    },
    deselectElement(){
      console.log('aaa')
      this.inputElement.isActive = false
      this.inputElement = undefined
    }
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
  margin: 60px 0 120px 0;
}

.table-wrapper{
  display: flex;
  list-style-type: none;
  flex-wrap: wrap;
  margin-bottom: 30px;
}


.flip-list-move {
  transition: transform 0.8s ease;
}
.flip-list-enter-active, .flip-list-leave-active {
  transition: opacity .5s;
}
.flip-list-enter, .flip-list-leave-to,{
  opacity: 0;
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
