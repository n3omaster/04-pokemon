<template>
    <div v-if="!pokemon">Cargando...</div>
    <div v-if="pokemon">
        <h1>¿Quién es este pokemon?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <PokemonOptions :pokemons="pokemonsArr" @selection="checkAnswer($event)" />

        <template v-if="showAnswer" class="fade-in">
            <h2>{{ resultMessage }}</h2>
            <button @click="newGame">Nuevo Juego</button>
        </template>
    </div>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions.vue";

// import helper
import getPokemonOptions from "../helpers/getPokemonOptions";

// run helper
// getPokemonOptions()

export default {
    methods: {
        revealPokemon() {
            this.showPokemon = true
            this.showAnswer = true
            this.resultMessage = "¡Correcto!"
        },
        loserAnswer() {
            this.showPokemon = true
            this.showAnswer = true
            this.resultMessage = `Ups, error, era ${ this.pokemon.name }`
        },
        checkAnswer(selectedPokemonId) {
            //console.log(selectedPokemonId);
            return (selectedPokemonId === this.pokemon.id) ? this.revealPokemon() : this.loserAnswer()
        },
        newGame() {
            // new Game Reset All
            pokemonsArr: []
            this.mixPokemonsArr()
            this.showPokemon = false
            this.showAnswer = false
            this.pokemon = null
        },
        async mixPokemonsArr() {
            this.pokemonsArr = await getPokemonOptions()
            const rndInt = Math.floor(Math.random() * 4)
            this.pokemon = this.pokemonsArr[rndInt]
        }
    },
    components: { PokemonPicture, PokemonOptions },
    data() {
        return {
            pokemonsArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            resultMessage: ""
        }
    },
    mounted() {
        //console.log('mounted')
        this.mixPokemonsArr()
    },
}
</script>
<style lang="">
    
</style>