<template>
    <TodoItem 
        v-for="(todo,index) in todos" 
        :key="index" 
        :todoProps="todo"
        @check-id="markItem"
    />
</template>

<script>
import {ref} from 'vue';
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",

    components:{TodoItem},

    setup() {
        const todos = ref([
            {
                id: 1,
                title: "Viec 1",
                complete: false
            },
            {
                id: 2,
                title: "Viec 2",
                complete: false
            },
            {
                id: 3,
                title: "Viec 3",
                complete: false
            }
            ]
        )

        const markItem = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id === id) todo.complete = !todo.complete
            })
            // console.log(todos);
        }
        
        return {
            todos,
            markItem
        };
    }
}
</script>

<style>

</style>