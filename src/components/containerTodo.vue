<template>
    <div>
        <div class="todo-wrapper">
            <h2>O que vai fazer hoje?</h2>
            <todoForm :todoList="todoList" @novoTodo="novoTodo"/>
            <p v-if="todoList.length === 0">Nenhum item montado</p>
            <todoList v-else v-for="todo in todoList" :key="todo.id" :todo="todo" @remover="deleteTodo" @todoToChange="findTodo" @showModal="handleModal"/>
        </div>
      <todoModal v-if="show" :show="show" @closeModal="handleModal" :patchTodo="patchTodo" @patchedText="addPatch"/>
    </div>
</template>

<script>


import todoForm from './todoForm.vue'
import todoList from './todoList.vue'
import todoModal from './todoModal.vue'

export default {
    data(){
        return {
            todoList: [],
            show: false,
            patchTodo: {}
        }
    },

    methods: {
         novoTodo(novoItemTodo){
            this.todoList.unshift(novoItemTodo)
            console.log(novoItemTodo)
         },
         addPatch(novoItem){
           const index = this.todoList.findIndex(x => x.id === novoItem.id)
           this.todoList.splice(index,1, novoItem)
         },
         deleteTodo(todo){
             const index = this.todoList.findIndex(x => x.id === todo.id)
             this.todoList.splice(index, 1)
         },
         handleModal(showEvent){
             this.show = showEvent
         },
        
        findTodo(todoItem){
             const index = this.todoList.findIndex(x => x.id === todoItem.id)
             this.patchTodo = this.todoList[index]
        },
        

         
    },
     
        
    components: {
        todoForm,
        todoList,  
        todoModal
    },

    watch: {
        todoList(newTodo){
            localStorage.todo = JSON.stringify(newTodo)
        }
    },

    mounted(){
        if(localStorage.todo){
            this.todoList = JSON.parse(localStorage.todo)
        }
    }

}
</script>

<style>
.todo-wrapper {
   display: flex;
   align-items: center;
   flex-direction: column;
   background: #1b1b1b;
   margin: 0 auto;
   min-height: 75vh;
   max-width: 50vw;
   padding: 2rem 0;
   border-radius: .8rem;
   color: #ffff;
   transition: max-width .2s, min-height .2s;
   position: relative;
}

body{
    background: linear-gradient(90deg,#144bff,#3e9deb);
    padding: 2rem 0;
    font-size: 1.4rem;
    position: relative;
}

* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    font-family: "Trebuchet MS","Lucida Sans Unicode","Lucida Grande","Lucida Sans",Arial,sans-serif
}

h2 {
    margin-bottom: 0.5rem;
    text-align: center;
}



@media(max-width: 600px){
   
    .todo-wrapper {
        max-width: 75vw;
        min-height: 75vh;
    }

    form input {
        padding: 1rem;
    }

    form button {
        padding: calc(1rem + 2px);
    
        width: 40%;
    }
}
</style>