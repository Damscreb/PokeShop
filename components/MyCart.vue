<template>
    <div v-click-outside="closeCart">
        <div class="shop-container">
            <div v-for="pokemon in cart" :key="pokemon.id">
                <div class="title">
                    <p>{{ pokemon.name }}</p>
                    <hr/>
                </div>
                <div class="price">
                    <p class="price-calcul">{{ quantityAndPrice(pokemon.quantity, pokemon.price) }}</p>
                    <p class="price-total">{{ totalPrice(pokemon.quantity, pokemon.price) }}</p>
                    <img src="~/assets/images/trash.png" alt="Bin's image">
                </div>
            </div>
            <div class="total">
                <p>TOTAL</p>
                <p>{{ totalPriceDollar }}</p>
                <div class="validate">Validate</div>
            </div>
        </div>
    </div>
</template>
<script>
import ClickOutside from 'vue-click-outside'
import Bus from '~/plugin/event-bus.js'
export default {
    computed: {
        totalPriceDollar () {
            return `${this.total}$`
        }
    },
    created () {
        this.cart = JSON.parse(localStorage.getItem('myCart'))
        Bus.$on('toggleCart', (toggleTrueFalse) => {
            this.toggle = toggleTrueFalse
        })

        this.total = this.cart.reduce(this.reducer, 0)
    },
    data () {
        return {
            cart: null,
            toggle: false,
            total: null
        }
    },
    methods: {
        closeCart () {
            if (this.toggle) {
                Bus.$emit('toggleOff', false)
            } else {
                this.toggle = true
            }
        },
        quantityAndPrice (quantity, price) {
            return `${quantity} x ${price}$`
        },
        reducer (callback, value) {
            return callback + (value.price * value.quantity)
        },
        totalPrice (quantity, price) {
            const totalPrice = quantity * price
            return `${totalPrice}$`
        }
    },
    directives: {
        ClickOutside
    }
}
</script>
<style lang="scss" scoped>
    .shop-container {
        position: absolute;
        z-index: 3;
        top: 80px;
        right: 0px;
        width: 500px;
        padding: 1em 2em;
        background-color: var(--color-white)
    }

    .title, .price, .total {
        display: flex;
        flex-direction: row;
        align-items: center;
        width: 100%;
    }

    .title {
        margin-bottom: 0.6em;
        & p {
            text-transform: capitalize;
            color: var(--color-black);
            letter-spacing: 1px;
            font-size: 1.1em;
            opacity: 80%;
        }
        & hr {
            width: 100%;
            height: 0px;
            margin-left: 1em;
            color: rgba(0, 159, 227, 0.2);
        }
    }

    .price {
        margin-bottom: 1.4em;
        justify-content: space-between;
        &-calcul {
            width: 100px;
            text-align: right;
            margin-left: 10em;
            opacity: 60%;
        }
        &-total {
            width: 50px;
            text-align: right;
            color: var(--color-black)
        }
        & img {
            width: 15px;
            opacity: 60%;
            &:hover {
                cursor: pointer;
            }
        }
    }

    .total {
        justify-content: space-between;
        padding-top: 1.3em;
        border-top: 5px solid rgba(0, 159, 227, 0.2);
        & p {
            width: 50%;
            text-align: right;
            color: var(--color-black);
            &:last-of-type {
                margin-right: 1.2em;
                color: var(--color-text-highlight);
            }
        }
        & .validate {
            padding: 0.5em 0.7em;
            color: var(--color-white);
            background-color: var(--color-text-highlight);
            border-radius: 5px;
            &:hover {
                cursor: pointer;
            }
        }
    }
</style>
