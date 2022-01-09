<template>
    <div class="shop-number">
        <div class="shop-container">
            <h3>{{ priceWithDollard }}</h3>
            <div class="add-buttons">
                <button class="minus" @click="removeQuantity()">
                    -
                </button>
                <p class="quantity">
                    {{ quantity }}
                </p>
                <button class="plus" @click="addQuantity()">
                    +
                </button>
            </div>
            <button class="cart">Add to cart</button>
        </div>
        <div class="number-container">
            <p class="pokemon-id">{{ numberReworked(number) }}</p>
        </div>
    </div>
</template>
<script>
export default {
    computed: {
        priceWithDollard () {
            return `$${this.$props.price}`
        }
    },
    data () {
        return {
            quantity: 1
        }
    },
    props: {
        number: {
            default: -1,
            type: Number,
            required: true
        },
        price: {
            default: -1,
            type: Number,
            required: true
        }
    },
    methods: {
        addQuantity () {
            this.quantity += 1
        },
        numberReworked (num) {
            const formatedNumber = num.toString().padStart(3, '0').padStart(4, '#')
            return formatedNumber
        },
        removeQuantity () {
            if (this.quantity >= 1) {
                this.quantity -= 1
            }
        }
    }
}
</script>
<style lang="scss" scoped>
    .shop-number {
        display: flex;
        flex-direction: row;
    }

    .shop-container {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-around;
        width: 100%;
    }

    h3 {
        font-size: 3em;
        color: var(--color-text-highlight);
    }

    .add-buttons {
        display: flex;
        flex-direction: row;
        border-radius: 5px;
        padding: 0.4em 0.5em;
        background-color: var(--color-white);
        color: var(--color-main-background-color);
        text-align: center;
    }

    .quantity {
        color: var(--color-text-highlight);
        font-size: 2.5em;
        width: 75px;
    }

    button {
        cursor: pointer;
        border: none;
        border-radius: 0;
    }

    .plus, .minus {
        width: 45px;
        height: 45px;
        font-size: 2.4em;
        background-color: #E5E5E5;
        color: var(--color-text-highlight);
    }

    .cart {
        font-size: 1.1em;
        padding: 0.8em 1em;
        border-radius: 5px;
        background-color: var(--color-text-highlight);
        color: var(--color-white);
    }

    .number-container {
        width: 100%;
        margin-left: 8em;
    }

    .pokemon-id {
        font-size: 15em;
        font-family: 'Roboto Italic';
        opacity: 50%;
    }
</style>
