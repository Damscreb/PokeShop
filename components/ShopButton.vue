<template>
    <div class="cart-block" @click.stop="openCart()">
        <img src="~/assets/images/cart.png" alt="Cart" />
        <p class="shop-text">Shopping cart</p>
        <div class="notification">
            <p>{{ notification }}</p>
        </div>
    </div>
</template>
<script>
import Bus from '~/plugin/event-bus.js'
export default {
    data () {
        return {
            notification: 0
        }
    },
    created () {
        const cartExist = localStorage.getItem('myCart')
        if (cartExist !== null) {
            const arrayPokemonQuantity = JSON.parse(localStorage.getItem('myCart')).map((data) => {
                return data.quantity
            })
            arrayPokemonQuantity.forEach((element) => {
                this.notification += element
                return element
            })
        } else {
            this.notification = 0
        }
        // Add some quantity
        Bus.$on('quantityDesired', (pokemonsData) => {
            this.notification += parseInt(pokemonsData.quantity)
        })
        // Remove some quantity
        Bus.$on('quantityRemoved', (minusNumber) => {
            this.notification -= minusNumber
        })
    },
    methods: {
        getPokemonsQuantity () {
            parseInt(JSON.parse(localStorage.getItem('myCart')).map((data) => {
                return data.quantity
            }))
        },
        openCart () {
            Bus.$emit('toggleCart', true)
        }
    }
}
</script>
<style lang="scss" scoped>
    .cart-block {
        display: flex;
        flex-direction: row;
        align-items: center;
        height: 100%;
        padding-left: 1em;
        border-left: 1px var(--color-text-highlight) solid;
        &:hover {
            cursor: pointer;
        }
    }

    img, .notification {
        width: 35px;
        height: 35px;
    }

    img {
        // To get the Cart png blue
        filter: invert(52%) sepia(46%) saturate(5251%) hue-rotate(169deg) brightness(97%) contrast(102%);
    }

    .shop-text {
        margin-inline: 1em;
    }

    .notification {
        background-color: var(--color-text-highlight);
        border-radius: 17px;
        & p {
            color: var(--color-white);
            width: max-content;
            margin: auto;
            position: relative;
            top: 25%;
        }
    }
</style>
