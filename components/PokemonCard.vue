<template>
    <div v-if="pokemon.id > 0" class="card">
        <img :src="pokemon.sprites.other.dream_world.front_default" :alt="`Une image de ${name}`"/>
        <h3>{{ name }}</h3>
        <p>{{ pokemon.id }}</p>
    </div>
</template>
<script>
export default {
    data () {
        return {
            pokemon: []
        }
    },
    async fetch () {
        if (this.$props.url) {
            // To get the right route of the pokemon... Not the best
            this.pokemon = await this.$axios.$get(`/${this.$props.url.split('v2/')[1]}`).then(response => response)
        }
    },
    props: {
        name: {
            default: 'Pikachu',
            type: String,
            require: true
        },
        url: {
            default: '/',
            type: String,
            require: true
        }
    }
}
</script>
<style scoped>
    .card {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-around;
        width: 200px;
        height: 300px;
        background: var(--color-white);
        box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
        border-radius: 5px;
        margin: 1em 0.5em;
    }

    .card:hover {
        cursor: pointer;
    }

    img {
        height: 50%;
        width: 80%;
    }

    h3 {
        text-transform: capitalize;
    }

    h3, p {
        color: var(--color-black);
    }
</style>
