<template>
    <div class="pokemon-list">
        <div v-for="pokemon in pokemonsList" :key="pokemon.name">
            <PokemonCard :name="pokemon.name" :url="pokemon.url"/>
        </div>
    </div>
</template>
<script>
import PokemonCard from '~/components/PokemonCard.vue'
export default {
    name: 'Home',
    components: {
        PokemonCard
    },
    data () {
        return {
            pokemonsList: []
        }
    },
    async fetch () {
        this.pokemonsList = await this.$axios.$get('/pokemon').then(response => response.results)
    }
}
</script>
<style scoped>
    .pokemon-list {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-around;
        align-items: center;
        margin: 1em;
    }
</style>
