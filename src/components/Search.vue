<template>
  <div class="search">
    <h1>{{msg}}</h1>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Digite algo e tecle enter..." v-model="query" />
    </form>
    <div v-if="results">
      <div v-for="result in results">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'search',
  data () {
    return {
      msg: 'Pesquise imagens oficiais da NASA',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult(query) {
      axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then( response => {
        this.results = response.data.collection.items;
      });
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
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
.search{
  margin:0 auto;
  width:100%;
}
.search img {
  max-width: 100%;
  min-width: 100%;
}
.search form input {
  margin-bottom:20px;
  width: 50%;
  padding:10px;
  border:1px solid grey;
}
</style>
