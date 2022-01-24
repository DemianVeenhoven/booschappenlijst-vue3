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
                <input v-model="grocery.amount" @input="calcGroceryTotal(grocery)"
                    type="number" min="0" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');">
            </td>
            <td>€{{grocery.total}}</td>
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
import { ref } from "vue";

//data
// TODO :: total is not needed in the grocery itself, cause it's data that can be computed
const groceries = ref([{name: "Bread", price: 0.99, amount: 0, total: 0}]);

// TODO :: make this computed
const absoluteTotal = ref(0);

//methods
const addGrocery = (newGrocery) => {
    // TODO :: newGrocery should be prepped in AddGrocery, not here
    newGrocery.name = newGrocery.name.charAt(0).toUpperCase() + newGrocery.name.slice(1);
    newGrocery.price = parseFloat(newGrocery.price).toFixed(2);
    newGrocery.amount = 0;
    newGrocery.total = 0;

    groceries.value.push(newGrocery)
}

// TODO :: method is not needed
const calcGroceryTotal = (grocery) => {
    grocery.total = parseFloat((grocery.amount * grocery.price)).toFixed(2);
    absoluteTotal.value = 0;

    groceries.value.forEach(element => {
        absoluteTotal.value = (parseFloat(absoluteTotal.value) + parseFloat(element.total)).toFixed(2)
    });
}
</script>

<style scoped>
    table, td {
        border: solid;
    }
</style>