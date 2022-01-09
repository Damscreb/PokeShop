<template>
    <div v-if="pokemon">
        <div class="poke-description">
            <NameAndType :pokename="pokemonName" :types="pokemonType"/>
            <Stats
                :pokename="pokemonName"
                :datas="pokemonDatas"
                :height="pokemon.height"
                :weight="pokemon.weight"
                :abilities="pokemonAbilities"
                :image="pokemon.sprites.other.dream_world.front_default
            "/>
        </div>
        <ShopAndNumber :price="pokemon.base_experience" :number="pokemon.id"/>
    </div>
</template>
<script>
import NameAndType from '~/components/pokemon/NameAndType.vue'
import ShopAndNumber from '~/components/pokemon/ShopAndNumber.vue'
import Stats from '~/components/pokemon/Stats.vue'
export default {
    components: {
        NameAndType,
        ShopAndNumber,
        Stats
    },
    data () {
        return {
            pokemon: null,
            pokemonAbilities: null,
            pokemonDatas: null,
            pokemonName: this.$route.params.pokename,
            pokemonType: null
        }
    },
    created () {
        // Axios call on the api with the name of the desired Pokemon
        this.$axios.$get(`/pokemon/${this.$route.params.pokename}`)
            .then((response) => {
                // We get the types of the Pokemon
                this.pokemonType = response.types.map((element) => {
                    return element.type.name
                })
                // We get the abilities of the Pokemon
                this.pokemonAbilities = response.abilities.map((element) => {
                    return element.ability.name
                })
                // We get the stats of the Pokemon
                this.pokemonDatas = response.stats.map((da) => {
                    const data = {
                        base_stat: da.base_stat,
                        name: da.stat.name
                    }
                    return data
                })
                // We get all the stats of the Pokemon
                this.pokemon = response
            })
            .catch((error) => {
                throw error
            })
    }
}
</script>
<style scoped>
    .poke-description {
        margin-top: 2em;
    }
</style>
