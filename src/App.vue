<template>
<div class="wrapper">

  <header class="header"><img style="width: 30px;" alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld class="wmf-wmui-color-green30" msg="Learn German with Wikidata Lexemes!" />
  </header>

  <aside class="aside aside-1"> 

<el-card shadow="hover" class="box-card">
  <template #header>
    <div class="clearfix">
      <span>German Lemma & Sense </span>

    </div>
  </template>
 <h3>  

  {{example[newRandomGermansense].lemma}}

   </h3> 


  <p class="body">  {{example[newRandomGermansense].sense}} </p>
     
      <el-button type="primary"  @click="createRandomGermanSense"> New Word </el-button>
</el-card>
    </aside>

   <article class="main">   

<el-card  shadow="hover" class="box-card">
  <template #header>
    <div class="clearfix">
      <span> Translate Here </span>

    </div>
  </template>

  
   <el-input  placeholder="Translition for the Word" v-model="newNativeTranslationLemma"  @keyup.enter="addTask"></el-input>
      <el-divider></el-divider>
     
 <el-input
  type="textarea"
  :autosize="{ minRows: 2, maxRows: 4}"
  placeholder="Please input"
  v-model="newNativeTranslationSense">
</el-input>

 <el-divider></el-divider>
 
 <el-button type="primary"  @click="addTranslation"> Save </el-button>
</el-card>
             
  </article>

  <footer class="footer"> 

<el-space wrap>
    <el-card shadow="hover" class="box-card" style="width: 250px" 
    v-for="translatedItem in translatedList" 
    :key="translatedItem.id">
      <template #header>
        <div class="clearfix">
          <h3>  {{ translatedItem.originalLemma }} </h3>
            <p class="body">  {{ translatedItem.originalSense }} </p>
       
        </div>
      </template>
      
          <p> {{translatedItem.translationLemma}} </p> 
            <p class="body"> {{translatedItem.translationSense}} </p> 
            <el-button type="primary"  @click="deleteTranslation(translatedItem.id)"> Delete </el-button>
           
    </el-card>
  </el-space>
 
  
    
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
      originalSenses: [],
      newRandomGermansense: '369',
      newNativeTranslationLemma: '',
      newNativeTranslationSense: '',
      translatedList: [],
  
    })
    

    const randomGermanSense = [Math.floor(Math.random() * state.example.length)]


    const createRandomGermanSense = () => {
      state.newRandomGermansense =  [Math.floor(Math.random() * state.example.length)]
      console.log(state.newRandomGermansense)
    }

    

    const addTranslation = () => {
       
      state.translatedList.push({
        id: uuid(),
        complete: false,
        edit: false,
        originalLemma: state.example[state.newRandomGermansense].lemma,
        originalSense: state.example[state.newRandomGermansense].sense,
        translationLemma: state.newNativeTranslationLemma,
        translationSense: state.newNativeTranslationSense
      })
      createRandomGermanSense()
      state.newNativeTranslationLemma = ''
        state.newNativeTranslationSense = ''
    }


        const deleteTranslation = taskId => {
      const translationIndex = state.translatedList.findIndex(task => task.id === taskId)
      state.translatedList.splice(translationIndex, 1)
    }
  

  
  return {
      ...toRefs(state),
      addTranslation,
      randomGermanSense,
      createRandomGermanSense,
      deleteTranslation
     
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

