<template>
    <main>
        <Header/>
        <div v-if="toggle" class="grey-filter"></div>
        <div class="content">
            <Nuxt/>
        </div>
    </main>
</template>
<script>
import Bus from '~/plugin/event-bus.js'
import Header from '~/components/Header.vue'
export default {
    components: { Header },
    created () {
        Bus.$on('toggleCart', (toggleTrueFalse) => {
            this.toggle = toggleTrueFalse
        })
        Bus.$on('toggleOff', (toggleTrueFalse) => {
            this.toggle = toggleTrueFalse
        })
    },
    data () {
        return {
            toggle: false
        }
    }
}
</script>
<style scoped>
    main {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        overflow: hidden;
        position: relative;
    }

    .content {
        max-width: 1200px;
        margin-inline: auto;
        height: auto;
        width: stretch;
    }

    .grey-filter {
        width: 100%;
        height: 100%;
        min-height: calc(100vh - 80px);
        position: absolute;
        top: 80px;
        z-index: 2;
        background-color: rgba(78, 77, 77, 0.452);
    }
</style>
