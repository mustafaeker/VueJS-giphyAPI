<template>
  <div id="app">

    <search 
      v-on:SearchRequested="handleSearch"
        ></search>
        <p v-if="isLoading">Loading</p>
    <preview 
      v-bind:gifs=gifs
    
    ></preview>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Preview from './components/Preview.vue'
export default {
name: 'app',
components:{ Search, Preview },

  data() {
    return{
      isLoading: true,
      gifs: []
    }
  },

  methods: {
    doQuery(url){
    fetch(url)
    .then ((res) => { 
        return res.json() 
    } )
    .then ((res) => { 
      this.gifs = res.data; 
      this.isLoading= false; 
     } )

    },
    handleSearch(query) {
    this.gifs = [];
    this.isLoading= true;
  
    const url = 'https://api.giphy.com/v1/gifs/search?q='+query+'&api_key=QJXyy9gfcL0Q2F3O1vUpAuOsIDGGtcAI&limit=25&offset=0&rating=G&lang=en';
    this.doQuery(url);
    

  

    }
  },

  created(){
   const url='https://api.giphy.com/v1/gifs/trending?api_key=UyK5OI1tzr7ZC5fM8nIw2lhmS9xdVw8q&limit=25&rating=G';
   this.doQuery(url);
  }
  
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}

</style>
