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
const emit = defineEmits(["add"])

const action = (payload) => {
    emit('add', payload);
}

const newGrocery = ref({
        name: null,
        price: null
});
</script>

<style scoped>

</style>