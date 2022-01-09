<template>
    <div class="name-type">
        <h1>{{ pokemonName.toUpperCase() }}</h1>
        <div class="type-container">
            <div v-for="type in pokemonType" :key="type" class="type" :ref="type">{{ type }}</div>
        </div>
    </div>
</template>
<script>
import colors from '~/plugin/pokemon-type-colours.js'
export default {
    data () {
        return {
            pokemonName: this.$props.pokename,
            pokemonType: this.$props.types
        }
    },
    mounted () {
        for (const type in this.$refs) {
            if (colors(type) !== '#777') {
                this.$refs[type][0].style.background = colors(type)
            }
        }
    },
    props: {
        pokename: {
            default: 'Pikachu',
            type: String,
            required: true
        },
        types: {
            type: Array,
            required: true
        }
    }
}
</script>
<style scoped lang="scss">
    .poke-description {
        margin-top: 2em
    }

    h1 {
        font-size: 4.5em;
        letter-spacing: 10px;
    }

    .name-type {
        display: flex;
        flex-direction: row;
    }

    .type-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-left: 1em;
    }

    .type {
        width: stretch;
        width: -moz-available;
        border-radius: 20px;
        font-size: .85em;
        margin: 0.2em 0;
        padding: .5em 1em;
        text-transform: uppercase;
        text-align: center;
        color: var(--color-main-background-color);
    }
</style>
