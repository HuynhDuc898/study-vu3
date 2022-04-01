<template>
    <AddTodo @add-todo="addTodo" />
    <TodoItem 
        v-for="(todo,index) in todos" 
        :key="index" 
        :todoProps="todo"
        @check-id="markItem"
        @delete-item="deleteItem"
    />
</template>

<script>
import {ref} from 'vue';
import TodoItem from './TodoItem.vue';
import AddTodo from './AddTodo.vue';
// import {v4 as uuidv4} from 'uuid';
import axios from 'axios';

export default {
    name: "Todos",

    components:{
        TodoItem,
        AddTodo
        },

    setup() {
        const todos = ref([
            
            ]
        )

        const getAllTodos = async () => {
            try {
                const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
                todos.value = res.data
            } catch (error) {
                console.log(error)
            }
        }

        getAllTodos();

        const markItem = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id === id) todo.complete = !todo.complete
                return todo
            })
            
        }
        const deleteItem = async id => {
        
            try {
                await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id)
            } catch (error) {
                console.log(error)
            }
        }

        const addTodo = async newTodo => {
            // todos.value.push(newTodo)
            try {
                const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo)
                todos.value.push(res.data)
            } catch (error) {
                
            }
        }
        
        return {
            todos,
            markItem,
            deleteItem,
            addTodo
        };
    }
}
</script>

<style>

</style>