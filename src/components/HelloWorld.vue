<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essa é uma lista de 20 pokemons vinda diretamente da <a target="_blank" href="https://pokeapi.co/api/v2/pokemon">API</a></h2>
    <h3 v-if="pokemonCount > 10">Quantidade de Pokemons: {{pokemonCount}}</h3>
    <button v-on:click="generatePokemons()">Ver outros Pokemons</button>
    <ul>
      <li v-for="pokemonName in pokemonNames" v-bind:key="pokemonName">{{pokemonName}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: {
      type: String,
      default: 'Título'
    }
  },
  // como um state inicial de variáveis do meu componente
  data() {
    return {
      pokemonNames: [],
      nextPagePokemonUrl: 'https://pokeapi.co/api/v2/pokemon'
    }
  },
  // aqui, colocamos variáveis que são dadas a partir de lógica simples
  computed: {
    pokemonCount() {
      return this.pokemonNames.length;
    }
  },
  // método do ciclo de vida que executa algo após a tema ser montada
  async mounted() {
    this.subtitle = 'Subtitulo após mounted';
    this.fetchApi();
  },
  // essas são os métodos que serão utilizados no meu componente
  methods: {
    fetchApi() {
      fetch(this.nextPagePokemonUrl)
        .then(response => response.json())
        .then(data => {
          this.nextPagePokemonUrl = data.next;
          this.sanitizePokemonNames(data.results)
        })
        .catch(err => console.log(err));
    },
    sanitizePokemonNames(pokemonList) {
      this.pokemonNames = pokemonList.map((pokemon) => pokemon.name);
    },
    generatePokemons() {
      this.fetchApi();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}

p {
  color: #2c3e50;
}
</style>
