<template>
    <div class="pokemon-container">
        <img :src="imgSrc" class="hidden-pokemon" alt="Pokemon IMG" />
        <img :src="imgSrc" class="fade-in" alt="Pokemon IMG" v-if="showPokemon" />
    </div>
</template>
<script>
export default {
    props: {
        pokemonId: {
            type: Number,
            default: 0,
            required: true
        },
        showPokemon: {
            type: Boolean,
            default: false,
            required: true
        }
    },
    name: 'PokemonPicture',
    data() {
        return {
            
        }
    },
    methods: {
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ this.pokemonId }.svg`
        }
    },
}
</script>
<style scoped>
/* Pokemon Picture */
.pokemon-container {
    height: 200px;
}

img {
    height: 200px;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.hidden-pokemon {
    filter: brightness(0);
}
</style>