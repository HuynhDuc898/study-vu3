<template>
    <TodoItem v-for="(todo,index) in todos" :key="index" :todoProps="todo"
    />
</template>

<script>
import {ref} from 'vue';
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",

    components:{TodoItem},

    setup() {
        const todos = ref(['Viec 1', 'Viec 2', 'Viec 3'])

        return {
            todos
        };
    }
}
</script>

<style>

</style>