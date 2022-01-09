<template>
    <div class="cart-block" @click="openCart()">
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
            cart: null,
            notification: 0
        }
    },
    created () {
        // We initialize our cart with the one saved in localStorage
        if (JSON.parse(localStorage.getItem('myCart')) && JSON.parse(localStorage.getItem('myCart')).length > 0) {
            this.cart = JSON.parse(localStorage.getItem('myCart'))
            this.cart.forEach((element) => {
                this.notification += element.quantity
            })
        }

        Bus.$on('quantityDesired', (pokemonsData) => {
            this.notification += pokemonsData.quantity

            // Add the quantity only in this.cart if the same pokemon is already in the cart
            if (this.cart) {
                const founded = this.cart.find(data => data.id === pokemonsData.id)
                if (founded) {
                    founded.quantity += pokemonsData.quantity
                } else {
                    this.cart.push(pokemonsData)
                }
            } else {
                this.cart = []
                this.cart.push(pokemonsData)
            }
            localStorage.setItem('myCart', JSON.stringify(this.cart))
        })
    },
    methods: {
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
        padding: 1em 0 1em 1em;
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
