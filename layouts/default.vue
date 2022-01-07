<template>
    <main>
        <Header/>
        <div class="content">
            <Nuxt/>
        </div>
    </main>
</template>
<script>
import Header from '~/components/Header.vue'
export default {
    components: { Header }
}
</script>
<style scoped>
    main {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    .content {
        max-width: 1200px;
        margin-inline: auto;
        height:auto;
    }
</style>
