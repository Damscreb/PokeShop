<template>
    <div>
        <header>
            <Nuxt-link to="/"><h1>R</h1></Nuxt-link>
            <ShopButton />
        </header>
        <MyCart/>
    </div>
</template>
<script>
import MyCart from '~/components/MyCart.vue'
import ShopButton from '~/components/ShopButton.vue'
export default {
    components: {
        MyCart,
        ShopButton
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
