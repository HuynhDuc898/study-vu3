<template>
    <div :class="['todoitem', todoProps.complete ? 'is-complete' : '']" >
        <input 
            type="checkbox"  
            :checked="todoProps.complete"
            @change="markItemComplete"
            >
        {{ todoProps.title }}
        <button class="red-btn">Delete</button>
    </div> 
</template>

<script>
export default {
    name: "TodoItem",
    props: ['todoProps'],
    
    setup(props, context) {
        const markItemComplete = () => {
            context.emit('check-id', props.todoProps.id)
        }

        return {
            markItemComplete
        }
    }

}
</script>

<style>
.red-btn {
    background: #ff0000;
    color: #ffff;
    border: none;
    padding: 2px;
    float: right;
    cursor: pointer;
    width: 70px;
    
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