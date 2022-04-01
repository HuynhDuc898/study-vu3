<template>
    <!-- <div :class="['todoitem', todoProps.completed ? 'is-complete' : '']" >
        <input 
            type="checkbox"  
            :checked="todoProps.completed"
            @change="markItemComplete"
            >
        {{ todoProps.title }}
        <button class="red-btn" @click="deleteItem">Delete</button>
    </div>  -->
    
    <tr>
        <td>{{todoProps.name}}</td>
        <td>{{todoProps.email}}</td>
        <td>{{todoProps.role.name}}</td>
        <td>
            <button class="btn-del" @click="deleteItem">Delete</button>
        </td>
    </tr>
</template>

<script>
export default {
    name: "TodoItem",
    props: ['todoProps'],
    
    setup(props, context) {
        const markItemComplete = () => {
            context.emit('check-id', props.todoProps.id)
        }
        const deleteItem = () => {
            context.emit('delete-item', props.todoProps.id)
        }

        return {
            markItemComplete,
            deleteItem,
            
        }
    },

}
</script>

<style>
.btn-del {
    background: rgb(240, 58, 58);
    color: #ffff;
    border: none;
    padding: 4px;
    cursor: pointer;
    width: 70px;
    border-radius: 5px;
    
}
.todoitem {
    margin-top: 2px;
    background: #f4f4f4;
    border-bottom: 1px #ccc dotted;
    height: 30px;
    line-height: 30px;
}
.is-complete {
    text-decoration: line-through;
}

</style>