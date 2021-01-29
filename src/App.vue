<template>
<div class="wrapper">
  <header class="header"><img style="width: 30px;" alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld class="wmf-wmui-color-green30" msg="Learn German with Wikidata Lexemes!" />
  </header>
 
  <aside class="aside aside-1"> 

<el-card shadow="hover" class="box-card">
  <template #header>
    <div class="clearfix">
      <span>A random German Word, used in an example sense: </span>

    </div>
  </template>
 <h3>  
<div v-if="newRandomGermansense === ''">
  {{example[randomGermanSense].lemma}}
</div>
<div v-else-if="newRandomGermansense !== ''">
  {{example[newRandomGermansense].lemma}}
</div>
   </h3> 

      
<div v-if="newRandomGermansense === ''">
   <p class="body">  {{example[randomGermanSense].sense}}  </p>
</div>
<div v-else>
  <p class="body">  {{example[newRandomGermansense].sense}} </p>
</div>

       
      <el-button type="primary"  @click="createRandomGermanSense"> New Word </el-button>
</el-card>
    </aside>



   <article class="main">   

<el-card  shadow="hover" class="box-card">
  <template #header>
    <div class="clearfix">
      <span> With Translation </span>

    </div>
  </template>
 <h3>  TEst </h3> 
      <p class="body">  In English: {{ newNativeTranslition }} </p>
</el-card>
          
     
  </article>
  
  
  <footer class="footer"> 
     <el-card shadow="hover">
           <el-input placeholder="Please input" v-model="newNativeTranslition"  @keyup.enter="addTask"></el-input>
 <el-button type="primary"  @click="addTask"> Save </el-button>
    </el-card>
    Test {{translatedList[0]}} 
   
    
    </footer>

    
</div>

 <!-- <li v-for="a in example" :key="a.sense">
      {{ a.sense }}
    </li> -->

</template>


<script>
import HelloWorld from "./components/HelloWorld.vue";
import { v4 as uuid } from 'uuid'
import json from '../public/sensewlemma.json'
import { reactive, toRefs} from 'vue'


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
      translatedList: [],
      newRandomGermansense: ''
    })
    

    const randomGermanSense = [Math.floor(Math.random() * state.example.length)]
    
    const createRandomGermanSense = () => {
      state.newRandomGermansense =  [Math.floor(Math.random() * state.example.length)]
      console.log(state.newRandomGermansense)
    }

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
      randomGermanSense,
      createRandomGermanSense
    }
    }
};
</script>


<style>
#app {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
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
  background: white;
}

.main {
  text-align: left;
  background: white;
}

.aside-1 {
  background: white;
  text-align: left;
  
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

.h3 {
  font-size: 18px;
  font-weight: 400;
  color: #2C3E50;

} 

p.body {
  color: #2C3E50;
  font-size: 14px;
  font-weight: 500;

}


</style>

