<template>
    <AddTodo @add-todo="addTodo" />
    <!-- <TodoItem 
        v-for="(todo,index) in todos" 
        :key="index" 
        :todoProps="todo"
        @check-id="markItem"
        @delete-item="deleteItem"
    /> -->

    <table class="list-user">
            <tr class="first-row">
                <th>Tên</th>
                <th>Email</th>
                <th>Vai trò</th>
                <th>Chức Năng</th>
            </tr>
            <TodoItem 
            v-for="(todo,index) in todos" 
            :key="index" 
            :todoProps="todo"
            @check-id="markItem"
            @delete-item="deleteItem"
            @search-user="searchUser"
            />
    </table>
</template>

<script>
import {ref, transformVNodeArgs} from 'vue';
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

        const getAllTodos = async (search = '') => {
            try {
                if(search)
                {
                    console.log('avcd')
                    const res = await axios.get(`http://127.0.0.1:8000/api/user/list?search=${search}`)
                    todos.value = res.data[0]
                }
                else
                {   
                    console.log('abc')
                    const res = await axios.get('http://127.0.0.1:8000/api/user/list')
                    todos.value = res.data[0]
                }
                
                
            } catch (error) {
                console.log(error)
            }
        }

        

        const searchUser = async (search) => {
            console.log(search)
            // try {
                
            //     todos.value = res.data[0]
            // } catch (error) {
            //     console.log(error)
            // }
        }
        searchUser();
        getAllTodos();
        const markItem = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id === id) todo.complete = !todo.complete
                return todo
            })
            
        }
        const deleteItem = async id => {
        
            try {
                // await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
                await axios.post('http://127.0.0.1:8000/api/user/soft/delete',{id})
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
            addTodo,
            searchUser
        };
    }
}
</script>

<style>
tr{
    /* border-bottom: 1px solid black; */
}
td, th {
    text-align: left;
}
.list-user {
    width: 100%;
    border-collapse: collapse;
}

.list-user, th, td {
    padding: 10px;
    /* border-bottom: 1px solid black; */
    font-size: 19px;
}

.first-row {
    background: #5f8ae7;
}

tr:nth-child(even) {background-color: #f2f2f2;}

</style>