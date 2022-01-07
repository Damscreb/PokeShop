<template>
    <div class="homepage">
        <div class="research">
            <p>Name</p>
            <input type="text" placeholder="Search by pokemon name" v-model="searchedPokemon" @input="filteredList" />
        </div>
        <div class="pokemon-list">
            <nuxt-link :to="`/pokemon/${pokemon.name}`" v-for="pokemon in pokemonsList" :key="pokemon.name">
                <PokemonCard :name="pokemon.name" :url="pokemon.url"/>
            </nuxt-link>
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
            pokemonsList: [],
            pokemonsListBasic: [],
            searchedPokemon: null
        }
    },
    methods: {
        filteredList () {
            // On renvoie des données seulement si on a mis 3 caractères minimum
            if (this.searchedPokemon.length >= 3) {
                this.pokemonsList = this.pokemonsListBasic.filter((pokemon) => {
                    return pokemon.name.toLowerCase().includes(`${this.searchedPokemon.toLowerCase()}`)
                })
            } else {
                this.pokemonsList = this.pokemonsListBasic
            }
        }
    },
    async fetch () {
        this.pokemonsListBasic = await this.$axios.$get('/pokemon').then(response => response.results)
        this.pokemonsList = this.pokemonsListBasic
    }
}
</script>
<style scoped>
    .homepage {
        text-align: center;
    }

    .pokemon-list {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-around;
        align-items: center;
        margin: 1em;
    }

    .research {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        margin-top: 2em;
    }

    .research p {
        margin-right: 0.5em;
        font-size: 2em;
        color: var(--color-text-highlight);
    }

    input {
        border: var(--color-black) solid 2px;
        border-radius: 3px;
        padding: 0.6em;
        width: 20em;
        outline: none
    }
</style>
