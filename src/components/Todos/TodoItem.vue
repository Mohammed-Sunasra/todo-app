<template>
    <base-card>
        <header><h2>{{ title }}</h2></header>
        <h3>Description: {{ description }}</h3>
        <p>Status: {{ status.toUpperCase() }}</p>
        <p>Priority: {{ priority.toUpperCase() }}</p>
        <base-button @click="deleteItem(id)">Delete</base-button>
    </base-card>
</template>

<script>
export default {
    props: ['id', 'title', 'description', 'status', 'priority'],
    emits: ['deleteTodo'],
    methods: {
        deleteItem(id){
            this.$emit('deleteTodo', id)
        }
    }
}
</script>