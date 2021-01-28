<template>
<div class="wrapper">
  <header class="header"><img style="width: 30px;" alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld class="wmf-wmui-color-green30" msg="Learn German with Wikidata Lexemes!" />
  </header>
 
  <aside class="aside aside-1"> {{example[12]}} </aside>


   <article class="main">    
      
   <input
        type="text"
        placeholder="Type a new todo item"
        class="new-task-input"
        v-model="newNativeTranslition"
        @keyup.enter="addTask"
      />
      <button class="new-task-button" @click="addTask">+ Add</button>
  
  </article>
  
  <aside class="aside aside-2"><p> In English: {{ newNativeTranslition }}</p> +  
  
  </aside>
  <footer class="footer"> Test {{translatedList[0]}} </footer>
</div>

 <!-- <li v-for="a in example" :key="a.sense">
      {{ a.sense }}
    </li> -->

</template>


<script>
import HelloWorld from "./components/HelloWorld.vue";
import { v4 as uuid } from 'uuid'
import json from '../public/sensewlemma.json'
import { reactive, toRefs, computed} from 'vue'

export default {
  name: "App",
  components: {
    HelloWorld
  },

  setup() {
    const state = reactive({
      example: json,
      newNativeTranslition: '',
      originalSenses: [],
      translatedList: []
    })

   const germanSenses = computed(() => {
      return state.originalSenses
    })
    
    const addTask = () => {
      state.translatedList.push({
        id: uuid(),
        complete: false,
        edit: false,
        label: state.newNativeTranslition
      })
      state.newNativeTranslition = ''
    }

  
  return {
      ...toRefs(state),
      addTask,
      germanSenses
    }
    }
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.wrapper {
  display: flex;  
  flex-flow: row wrap;
  font-weight: bold;
  text-align: center;
}

.wrapper > * {
  padding: 10px;
  flex: 1 100%;
}

.header {
  background: white;
}

.footer {
  background: lightgreen;
}

.main {
  text-align: left;
  background: deepskyblue;
}

.aside-1 {
  background: gold;
}

.aside-2 {
  background: hotpink;
}

@media all and (min-width: 600px) {
  .aside { flex: 1 0 0; }
  
}

@media all and (min-width: 800px) {
  .main    { flex: 1 0px; }
  .aside-1 { order: 1; } 
  .main    { order: 2; }
  .aside-2 { order: 3; }
  .footer  { order: 4; }
}

body {
  padding: 2em; 
}


</style>

