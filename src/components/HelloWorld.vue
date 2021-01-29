<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      A random German <a href="https://simple.wikipedia.org/wiki/Lemma_(linguistics)"> lemma</a> is displayed here with an example <a href="https://www.wikidata.org/wiki/Wikidata:Lexicographical_data/Documentation"> sense</a>, <br />
      you can translate it to learn some new German vocabulary. <br />
      All the edits are only visible to you, so feel free to make mistakes! <br />
     
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
p {
  color: #2C3E50;
  font-size: 14px;
  font-weight: 500;

}
</style>
