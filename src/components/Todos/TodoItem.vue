<template>
    <base-card>
        <header><h2>{{ title }}</h2></header>
        <h3>Description: {{ description }}</h3>
        <p>Status: {{ status.toUpperCase() }}</p>
        <p>Priority: {{ priority.toUpperCase() }}</p>
        <base-button @click="deleteTodoItem(id)">Delete</base-button>
    </base-card>
</template>

<script>
export default {
    props: ['id', 'title', 'description', 'status', 'priority'],
    methods: {
        deleteTodoItem(){

        }
    }
}
</script>