<template>
    <div class="container mb-3">
        <header class="head">
            <h1 class="heading">
                Todo List
            </h1>
        </header>
        <section class="todo-body">
            <form action="">
                <div class="mb-4 todoTop">
                    <input type="text" class="form-control p-2" placeholder="Enter Todo" v-model="inputValue">
                    <button class=" btn btn-primary p-2" @click.prevent="AddTodo()">Add Todo</button>
                </div>
            </form>
            <ul  class="item-list" >
                <li  class="item">Default Todo</li>
                <li v-for="(todo,index) in todoList" class="item" :key="index">{{ todo?.text }} 
                    <input type="checkbox" class="form-check-input" v-model="completed">
                </li>
            </ul>
        </section>
    </div>
</template>

<script>
export default {
    created(){
        this.getTodoList()
    },
    data(){
        return {
            todoList:[],
            completed:false,
            inputValue:""
        }
    },
    methods:{
       async getTodoList(){
        let todos=await fetch("Todo.json")
        todos=await todos.json()
        if(todos){
            this.todoList=todos
        }
        console.log(todos)
        },
        AddTodo(){
            let id=new Date().getMilliseconds()
            if(this.inputValue.length>0){
                this.todoList.push({
                    text:this.inputValue,
                    id:id,
                    isDone:this.completed
                })
            }
            this.inputValue=""
        }

    },
}
</script>
<style>
.todoTop{
    display: flex;
    gap: 2em;
}
.todo-body{
    display: flex;
    flex-direction: column;
    gap: 2em;
}
.item{
    color: #544e4e;
    font-weight: 500;
    font-size: 1.2em;
}
</style>