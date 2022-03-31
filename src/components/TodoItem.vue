<template>
    <div class="todoitem">
        <input type="checkbox" >
        {{ todoProps }}
        <button class="red-btn">Delete</button>
    </div> 
</template>

<script>
export default {
    name: "TodoItem",
    props: ['todoProps']
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

</style>