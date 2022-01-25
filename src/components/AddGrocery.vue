<template>
    <label>Name:</label>
    <input v-model="newGrocery.name"/>

    <br>
    <br>

    <label>Price: €</label>
    <input v-model.number="newGrocery.price"
        placeholder="0.00" inputmode="decimal" onkeypress="return (event.charCode >= 48 && event.charCode <= 57) ||  event.charCode == 46 || event.charCode == 0 "
    />
    
    <br>
    <br>

    <button @click="action()">Add grocery</button>
</template>

<script setup>
import { reactive } from "vue";

const emit = defineEmits(["add"]);

const newGrocery = reactive({
    name: null,
    price: null,
    amount: 0
});

const action = () => {
    const createdGrocery = {...newGrocery}
    createdGrocery.name = createdGrocery.name.charAt(0).toUpperCase() + createdGrocery.name.slice(1);
    createdGrocery.price = parseFloat(createdGrocery.price).toFixed(2);

    emit('add', createdGrocery);

    newGrocery.name = null;
    newGrocery.price = null;
}
</script>

<style scoped>

</style>