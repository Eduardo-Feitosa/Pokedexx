<template>
  <div id="app">
    
    <img src="@/assets/pokcapa.jpg">
    <h1 class="is-size-3" >Pokedex</h1>
    <input type="text"  class="input is-rounded " v-model="busca" placeholder="Procure seu pokemon" id="ib">
    <button class="button is-medium is-fullwidth is-success" id="botB" @click="buscar">pesquisar</button>
    <hr>
    
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke,index) in filPoke" :key="poke.url">
        <PokemonComp :name ="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>   
  </div>
</template>

<script>
import axios from 'axios';
import  PokemonComp from './components/PokemonComp.vue'
export default { 
 name: 'App',
 data(){
    return{
    pokemons:[],
    filPoke: [],
    busca: ''
    }
  }
,
  //ele irá chamar essa função quando for criado
  created: function(){
   axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Pegou os dados pokemon");
      this.pokemons = res.data.results;
      this.filPoke = res.data.results;
   })
  },
  components: {
    PokemonComp
  },
  methods:{
    buscar: function(){
      this.filPoke = this.pokemons;
      if(this.busca == '' || this.busca == ' ' ){
        this.filPoke = this.pokemons;
      }else{
          this.filPoke = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
      
    }

    }
  }
   /*computed: {
   
    result: function (){
      if(this.busca == '' || this.busca == ' ' ){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
      
    }*/
  
  

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
#ib{
  width: 500px;
  margin-bottom: 2%;
 

  
}
#botB{
 
  margin-top: 2%;
  margin: auto;
  width: 55%;
  border-radius: 20px;

}

</style>
