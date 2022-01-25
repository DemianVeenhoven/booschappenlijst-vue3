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

    <AddGrocery @add="groceries.push($event)"/>
</template>

<script setup>
import AddGrocery from "./AddGrocery.vue";
import { computed, ref} from "vue";

//data
const groceries = ref([{name: "Bread", price: 0.99, amount: 0}]);

//computed
const absoluteTotal = computed(() => {
    return groceries.value.reduce((acc, {price,amount}) => acc += price * amount, 0).toFixed(2)
})
</script>

<style scoped>
    table, td {
        border: solid;
    }
</style>