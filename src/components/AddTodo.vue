<template>
  <!-- <form @submit.prevent="addItem"> -->
  <form @submit.prevent="searchList">
      <input type="text" placeholder="Nhap tu tim kiem ..." v-model="title" >
      <input type="submit" value="Search" class="add-btn">
  </form>
  <!-- <div><button class='btn-add'>Add</button></div> -->
</template>

<script>
import {ref} from 'vue';
// import {v4 as uuidv4} from 'uuid';

export default {
    name: "AppTodo",
    
    setup(props, context) {
        const title = ref('');

        const addItem = event => {
            const newItem = {
                // id: uuidv4(),
                title: title.value,
                completed: false
            }

            context.emit('add-todo', newItem);
            title.value = '';
        }

        const searchList = () => {
            // console.log(title.value)
            context.emit('search-user', title.value)
        } 
        
        return {
            title,
            addItem,
            searchList
            
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}

input[type='text'] {
    flex: 10;
    padding: 5px;
}

input[type='submit'] {
    flex: 2;
}
.btn-add {
    float: right;
    background: red;
    z-index: 2;
}
</style>