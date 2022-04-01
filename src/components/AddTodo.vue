<template>
  <form @submit.prevent="addItem">
      <input type="text" placeholder="Viec lam...." v-model="title" >
      <input type="submit" value="Thêm" class="add-btn">
  </form>
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
        
        return {
            title,
            addItem
            
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
</style>