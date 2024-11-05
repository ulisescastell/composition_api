<script>
import CartCmp from './CartCmp.vue';
import { provide, ref } from 'vue';

export default {
    components: {
        CartCmp
    },
    setup() {
        const currency = ref('USD');
        const orderName = ref('');
        const orderTitle = ref('');
        const products = [
            { name: "Hamburger 🍔", price: 5 },
            { name: "Cheeseburger 🧀", price: 6 },
            { name: "Nuggets 🥕", price: 7 },
            { name: "Fries 🍟", price: 2 }
        ];

        const addToCart = (product) => {
            alert(`${product.name} added to order`);
        }

        const placeOrder = () => {
            if (orderName.value.trim()) {
                orderTitle.value = `Order: ${orderName.value}`
                alert(`Order ${orderName.value} has been placed!`)
            } else {
                alert("Please enter an order name")
            }
        }

        provide('addToCart', addToCart)

        return {
            orderName,
            orderTitle,
            products,
            placeOrder,
            currency
        }
    }
}
</script>

<template>
    <main>
        <div class="mainContainer">
            <h1>{{ orderTitle || "Order name will be displayed once order is confirmed" }}</h1>
            <input type="text" v-model="orderName" placeholder="Type your order name...">
            <button @click="placeOrder">Place order</button>
            <label for="currency">
                <select v-model="currency" name="currency"> Currency
                    <option value="USD">Dolars ($)</option>
                    <option value="EUR">Euros (€)</option>
                </select>
            </label>

            <br>
            <br>
            <div v-for="(product, index) in products" :key="index">
                <CartCmp :product="product" :currency="currency" />
            </div>
        </div>
    </main>
</template>

<style scoped>
.mainContainer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>
