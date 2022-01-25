<template>
    <label>Name:</label>
    <input v-model="newGrocery.name"/>

    <br>
    <br>

    <label>Price: €</label>
    <input v-model="newGrocery.price"
        placeholder="0.00" inputmode="decimal" onkeypress="return (event.charCode >= 48 && event.charCode <= 57) ||  event.charCode == 46 || event.charCode == 0 "
    />
    
    <br>
    <br>

    <button @click="action(newGrocery)">Add grocery</button>
</template>

<script setup>
import { ref } from "vue";

// emits: [ "add" ],
const emit = defineEmits(["add"]);


const newGrocery = ref({
        name: null,
        price: null
});

const action = (payload) => {
    const createdGrocery = JSON.parse(JSON.stringify(payload));
    createdGrocery.name = createdGrocery.name.charAt(0).toUpperCase() + createdGrocery.name.slice(1);
    createdGrocery.price = parseFloat(createdGrocery.price).toFixed(2);
    createdGrocery.amount = 0;

    emit('add', createdGrocery);

    newGrocery.value.name = null;
    newGrocery.value.price = null;
}
</script>

<style scoped>

</style>