<script>
import { inject, computed } from 'vue';

export default {
    props: {
        product: {
            type: Object,
            required: true
        },
        currency: {
            type: String,
            required: true
        }
    },
    setup(props) {


        const addToCart = inject('addToCart');

        const handleAddToCart = () => {
            addToCart(props.product)
        }

        const formattedPrice = computed(() => {
            const rate = props.currency === 'EUR' ? 0.85 : 1;
            const symbol = props.currency === 'EUR' ? '€' : '$';
            return `${symbol}${(props.product.price * rate).toFixed(2)}`;
        });

        return {
            handleAddToCart,
            formattedPrice

        }
    }
}
</script>

<template>
    <div class="container">
        <label :for="product.name">
            {{ product.name }} - {{ formattedPrice }}
            <button @click="handleAddToCart">Add to cart</button>
        </label>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    max-width: 300px;
    gap: 10px;
    justify-content: center;
    align-items: center;
}
</style>
