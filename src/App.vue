<template>
<div class="wrapper">

  <header class="header">
  <HelloWorld class="wmf-wmui-color-green30" msg="Learn German with Wikidata Lexeme" />
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
       
        <el-divider></el-divider>
         <div style="margin: 32px 0;"></div>
      <el-button type="primary"  @click="createRandomGermanSense" icon="el-icon-refresh-left" primary plain> New Lemma & Sense </el-button>
         
</el-card>
    </aside>

   <article class="main">   


<el-card  shadow="hover" class="box-card">
  <template #header>
    <div class="clearfix">
      <span> Translate Here </span>

    </div>
  </template>

  
   <el-input  placeholder="Translation for the word" v-model="newNativeTranslationLemma"  @keyup.enter="addTask"></el-input>
     
     <div style="margin: 16px 0;"></div>
 <el-input
  type="textarea"
  :autosize="{ minRows: 2, maxRows: 4}"
  placeholder="Please translate the sense here."
  v-model="newNativeTranslationSense"
  >
</el-input>
<div style="margin: 32px 0;"></div>
 <!-- <el-divider></el-divider> -->
 
 <el-button type="primary"  icon="el-icon-plus" @click="addTranslation"> Add Translation </el-button>
</el-card>
             
  </article>

  <footer class="footer"> 

<el-space wrap>
    <el-card shadow="hover" class="box-card translatedCard" style="width: 250px" 
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
              <el-button type="danger" @click="deleteTranslation(translatedItem.id)" icon="el-icon-delete" circle></el-button>
           
    </el-card>
  </el-space>
<p class="smally"> 
  LearnGermanwithLexeme 1.0 by Erdi , Source of the data: 
  <a href='https://query.wikidata.org/#%23Lexemes%20in%20Swedish%20with%20usage%20example%20that%20demonstrates%20both%20a%20form%20and%20a%20sense%0A%23Lexemes%20in%20Swedish%20with%20usage%20example%20that%20demonstrates%20both%20a%20form%20and%20a%20sense%0A%23%20So9q%2023-12-2020%0Aselect%20%20%3Fsense%20%3Flemma%20%0AWHERE%20%7B%0A%20%20%3FlexemeId%20%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2Flanguage%3E%20wd%3AQ188%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20wikibase%3Alemma%20%3Flemma%20%3B%0A%20%20%20%20%20%20%20%20%20%20%20%23%20ontolex%3Asense%20%3Fsense%20.%0A%20%20%20%20%20%20%20%20%20ontolex%3Asense%2Fskos%3Adefinition%20%3Fsense%20.%20%0A%0A%7D'> Wikidata (query) </a>
  Inspired by tools listed <a href="https://www.wikidata.org/wiki/Wikidata:Tools/Lexicographical_data"> here </a>.
  <a href="https://github.com/erdincciftci"> Github </a>
  </p>

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

.translatedCard {
background-color: #f8f9fa;
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

p.smally {
  color: #2c3e50;
  font-size: 12px;
  font-weight: 500;

}


</style>

