<template>
    <base-card>
    <div>
        <label for=""></label>
        <header>{{ title }}</header>
        <p>{{ description }}</p>
        <p>{{ status }}</p>
        <p>{{ priority }}</p>
        <base-button @click="deleteTodoItem(id)">Delete</base-button>
    </div>
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