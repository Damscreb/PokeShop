<template>
    <div>
        <header>
            <Nuxt-link to="/"><h1>R</h1></Nuxt-link>
            <ShopButton />
        </header>
        <MyCart v-if="toggle"/>
    </div>
</template>
<script>
import Bus from '~/plugin/event-bus.js'
import MyCart from '~/components/MyCart.vue'
import ShopButton from '~/components/ShopButton.vue'
export default {
    components: {
        MyCart,
        ShopButton
    },
    data () {
        return {
            toggle: false
        }
    },
    created () {
        Bus.$on('toggleCart', (toggleTrueFalse) => {
            this.toggle = toggleTrueFalse
        })
        Bus.$on('toggleOff', () => {
            this.toggle = false
        })
    }
}
</script>
<style scoped>
    header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        padding-inline: 2em;
        background-color: #fff;
        max-width: 100%;
        height: 80px;
        box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.15);
        position: relative;
    }

    h1 {
        font-family: 'Roboto Bold';
        color: var(--color-text-highlight);
        font-size: 4em;
    }
</style>
