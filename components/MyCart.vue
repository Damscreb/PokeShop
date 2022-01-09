<template>
    <div v-click-outside="closeCart">
        <div class="shop-container">
            <p>Hello</p>
            <p>Goodbye</p>
        </div>
    </div>
</template>
<script>
import ClickOutside from 'vue-click-outside'
import Bus from '~/plugin/event-bus.js'
export default {
    created () {
        Bus.$on('toggleCart', (toggleTrueFalse) => {
            this.toggle = toggleTrueFalse
        })
    },
    data () {
        return {
            toggle: false
        }
    },
    methods: {
        closeCart () {
            if (this.toggle) {
                Bus.$emit('toggleOff', false)
            } else {
                this.toggle = true
            }
        }
    },
    directives: {
        ClickOutside
    }
}
</script>
<style lang="scss" scoped>
    .shop-container {
        position: fixed;
        z-index: 3;
        top: 80px;
        right: 0px;
        width: 500px;
        padding: 1em;
        background-color: var(--color-white)
    }
</style>
