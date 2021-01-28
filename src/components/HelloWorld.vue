<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Learn German with translating lexemes in German to your own native language!  <br />
      Nothing made here effects Wikidata, so... Feel free to play around!
     
    </p>
   
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
