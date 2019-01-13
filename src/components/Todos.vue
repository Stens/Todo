<template>
    <div>
        <div class="title">
            <h1>Things you need to do</h1>
        </div>

        <div v-bind:key="todo.id" v-for="todo in todos"> <!-- For loop, needs key to keep track of elements -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"]
}
</script>

<style scoped>
    .title {
        text-align: center;
    }

</style>

