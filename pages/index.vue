<template>
    <div class="homepage">
        <div class="research">
            <p>Name</p>
            <input type="text" placeholder="Search by pokemon name" v-model="searchedPokemon" @input="filteredList" />
        </div>
        <div class="quantity">
            <label for="quantity-pokemon">Number of pokemons displayed:</label>
            <select v-model="quantityDisplayed" id="quantity-pokemon">
                <option :value="20" @click="$fetch">20</option>
                <option :value="40" @click="$fetch">40</option>
                <option :value="60" @click="changeList(60)">60</option>
                <option :value="80" @click="changeList(80)">80</option>
            </select>
        </div>
        <div v-if="pokemonsList.length === quantityDisplayed" class="pokemon-list">
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
            quantityDisplayed: 20,
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
    }, // TRAVAIL EN COURS, Raccourcir ou rallonger pokemonslList
    async fetch () {
        if (this.pokemonsList.length >= this.quantityDisplayed) {
            this.pokemonsList.length = this.quantityDisplayed
        }
        this.pokemonsListBasic = await this.$axios.$get('/pokemon?offset=0&limit=80').then(response => response.results)
        this.pokemonsList = this.pokemonsListBasic
        this.pokemonsList.length = this.quantityDisplayed
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
