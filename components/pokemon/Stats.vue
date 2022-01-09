<template>
    <div class="stats-container">
        <div class="stats">
            <p>{{ pokemonHeight }}</p>
            <p>{{ pokemonWeight }}</p>
            <p>Abilities:
                <ul>
                    <li v-for="ability in abilities" :key="ability">{{ ability }}</li>
                </ul>
            </p>
        </div>
        <div class="datas">
            <DataBar v-for="data in datas" :key="data.name" :name="data.name" :base_stat="data.base_stat"/>
        </div>
        <img :src="image" :alt="imageAlt"/>
    </div>
</template>
<script>
import DataBar from '~/components/pokemon/DataBar.vue'
export default {
    components: { DataBar },
    computed: {
        imageAlt () {
            return `Une image de ${this.$props.pokename}`
        },
        pokemonHeight () {
            const height = this.$props.height / 10
            return `Height: ${height}m`
        },
        pokemonWeight () {
            const weight = this.$props.weight / 10
            return `Weight: ${weight}kg`
        }
    },
    props: {
        abilities: {
            default: null,
            type: Array,
            required: true
        },
        datas: {
            default: null,
            type: Array,
            required: true
        },
        height: {
            default: -1,
            type: Number,
            required: true
        },
        image: {
            default: '',
            type: String,
            required: true
        },
        pokename: {
            default: '',
            type: String,
            required: true
        },
        weight: {
            default: -1,
            type: Number,
            required: true
        }
    }
}
</script>
<style scoped lang="scss">
    .stats {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        width: 18%;
        padding: 1em 0;
        &-container {
            display: flex;
            flex-direction: row;
            justify-content: unset;
            width: 100%;
        }
        & p {
            font-size: 1.4em;
            &:not(:last-of-type) {
                margin-bottom: 1em;
            }
        }
    }

    li {
        font-size: 0.7em;
        list-style: disc inside;
        text-transform: capitalize;
        margin: 0.5em 0;
    }

    .datas {
        height: max-content;
        border-left: 1px solid rgba(0, 159, 227, 0.25);
        padding: 1em 0 1em 4em;
    }

    img {
        height: 25em;
        width: 25em;
        position: absolute;
        z-index: 1;
        right: 130px;
        top: 120px;
    }
</style>
