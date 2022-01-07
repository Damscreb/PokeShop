<template>
    <div>
        {{ pokemonName }}
    </div>
</template>
<script>
export default {
    data () {
        return {
            pokemonName: null
        }
    },
    mounted () {
        this.pokemonName = this.$route.params.pokename
    }
}
</script>
