<template>
  <div class="container">
    <div class="row">
    <div v-for="pokemon in pokemonList" v-bind:key="pokemon">
      
        <div class="col">
          <div class="card" style="width: 18rem;">
            <img class="card-img-top" :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png`" alt="Card image cap">
            <div class="card-body">
              <h5 class="card-title">{{ pokemon.name }}</h5>
              <span v-for="tipo in pokemon.types" v-bind:key="tipo">
                <p class="card-text">{{ tipo.type.name }}</p>
              </span>
              <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const obterPokemonList = () => {
  const url = id => `https://pokeapi.co/api/v2/pokemon/${id}`
  const listaPromeses = []
  for (let i = 1; i <= 20; i++) {
    listaPromeses.push(
      fetch(url(i))
        .then(response => response.json())
    )
  }
  return Promise.all(listaPromeses)

}

export default {
  name: 'HomePage',
  data() {

    return {
      brand: 'pokemon',
      pokemonList: {},
      nomePokemon: '',

    }

  },
  methods: {

  },
  mounted() {
    obterPokemonList().then(data => {
      this.pokemonList = data
      this.nomePokemon = data.length
      console.log(data);
    })
  },
  computed: {
    obterNomes() {
      if (this.pokemonList.length > 0) {
        let lista = this.pokemonList
        let result = lista.filter(t => t.name == 'o que o usuario digitar')
        console.log(result);
        return result
      }
      return []

    }
  }

}
</script>

<style scoped>

</style>
