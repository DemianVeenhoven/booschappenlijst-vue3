<template>
    <h1>GroceryList</h1>

    <table>
        <tr>
            <th>Name</th>
            <th>Price</th>
            <th>Amount</th>
            <th>Total</th>
        </tr>

        <tr v-for="grocery in groceries" :key="grocery.name">
            <td>{{grocery.name}}</td>
            <td>€{{grocery.price}}</td>
            <td>
                <input v-model="grocery.amount"
                    type="number" min="0" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');">
            </td>
            <td>€{{(grocery.price * grocery.amount).toFixed(2)}}</td>
        </tr>

        <tr>
            <td colspan="3">Total:</td>
            <td>€{{absoluteTotal}}</td>
        </tr>
    </table>

    <br>

    <AddGrocery @add="addGrocery($event)"/>
</template>

<script setup>
import AddGrocery from "./AddGrocery.vue";
import { computed, ref, watchEffect } from "vue";

//data
const groceries = ref([{name: "Bread", price: 0.99, amount: 0}]);

//computed
const groceryTotal = (grocery) => computed(() => {
    if (grocery.amount) {
        return parseFloat((grocery.amount * grocery.price).toFixed(2));
    }

    return 0;
});

const absoluteTotal = computed(() => {
    const groceriesTotal = [];
    const reducer = function(total, num) {
        return total + num;
    }

    groceries.value.forEach(grocery => {
        groceriesTotal.push(parseFloat((grocery.price * grocery.amount).toFixed(2)));
    });
    
    return (groceriesTotal.reduce(reducer)).toFixed(2);
});

//methods
const addGrocery = (newGrocery) => {
    groceries.value.push(newGrocery)
}
</script>

<style scoped>
    table, td {
        border: solid;
    }
</style>