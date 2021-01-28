<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Learn German with Wikidata Lexemes!" />
 {{example[1]}}
 <li v-for="a in example" :key="a.sense">
      {{ a.sense }}
    </li>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import json from '../public/sensewlemma.json'

export default {
  name: "App",
  components: {
    HelloWorld
  },
 data() {
    return {
      example : json
      
    }
  },
 mounted() {

  json.forEach(x => { console.log(x.lemma, x.sense); });

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
</style>
