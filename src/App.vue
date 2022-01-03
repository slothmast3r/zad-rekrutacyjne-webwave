<template>
  <div id="app">
    <transition-group name="flip-list" tag="div" class="table-wrapper">
      <tab-element
          v-for="el in kontener"
          :key="el.id"
          :columns-count="columnsCount"
          :is-active="el.isActive"
          :title="el.title"
          @component-clicked="selectElement(el)"
      />
    </transition-group>
    <button @click="kontener = shuffle(kontener);">Shuffle</button>
    <input v-model="inputElement.title">
  </div>
</template>

<script>


import TabElement from "@/components/TabElement";
export default {
  name: 'App',
  components: {
    TabElement
  },
  data(){
    return {
      kontener: [],
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
      for (let i = 0; i < this.elementsCount; i++) {
        let obj = {
          title : 'Tytuł '+ (i+1),
          id : 'kontener' + i,
          isActive: false,
        }
        this.kontener.push(obj)
      }
    },
    shuffle(array) {
      let currentIndex = array.length,  randomIndex;

      while (currentIndex != 0) {

        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [array[currentIndex], array[randomIndex]] = [
          array[randomIndex], array[currentIndex]];
      }
      return array;
    },
    selectElement(el){
      this.inputElement.isActive = false
      this.inputElement = el
      this.inputElement.isActive = true
    },
    deselectElement(){
      this.inputElement = false
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
</style>
