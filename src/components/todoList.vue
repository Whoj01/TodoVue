<template>
     <div class="row" :class="[todoItem.completed ? 'completed' : ''] ">
        <div class="todo-text" @click="todoItem.completed = !todoItem.completed">{{todoItem.texto}}</div>
        <div> 
            <svg xmlns="http://www.w3.org/2000/svg"  @click="deleteMessage" class='delete' id="Outline" viewBox="0 0 24 24" width="32" height="32"><path d="M16,8a1,1,0,0,0-1.414,0L12,10.586,9.414,8A1,1,0,0,0,8,9.414L10.586,12,8,14.586A1,1,0,0,0,9.414,16L12,13.414,14.586,16A1,1,0,0,0,16,14.586L13.414,12,16,9.414A1,1,0,0,0,16,8Z"/><path d="M12,0A12,12,0,1,0,24,12,12.013,12.013,0,0,0,12,0Zm0,22A10,10,0,1,1,22,12,10.011,10.011,0,0,1,12,22Z"/></svg>
            <svg xmlns="http://www.w3.org/2000/svg" @click="openModal"  class="change" viewBox="0 0 24 24" width="32" height="32"><g id="_01_align_center" data-name="01 align center"><path d="M5,19H9.414L23.057,5.357a3.125,3.125,0,0,0,0-4.414,3.194,3.194,0,0,0-4.414,0L5,14.586Zm2-3.586L20.057,2.357a1.148,1.148,0,0,1,1.586,0,1.123,1.123,0,0,1,0,1.586L8.586,17H7Z"/><path d="M23.621,7.622,22,9.243V16H16v6H2V3A1,1,0,0,1,3,2H14.758L16.379.379A5.013,5.013,0,0,1,16.84,0H3A3,3,0,0,0,0,3V24H18.414L24,18.414V7.161A5.15,5.15,0,0,1,23.621,7.622ZM18,21.586V18h3.586Z"/></g></svg>
        </div>
        
    </div>
    
</template>

<script>
//import { eventBus } from './../main'

export default {
    data(){
        return {
            todoItem: this.todo,
            show: false
        }
    },

   
    props: {
        todo: {
            type: Object,
            required: true
        }
    },

    methods: {
        deleteMessage(){
             this.$emit('remover', this.todoItem)
             
            },
        openModal(){
            this.show = true
            this.$emit('showModal', this.show)
            this.$emit('todoToChange', this.todoItem)
        }
    }
}
</script>

<style>
.row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 90%;
    padding: .8rem;
    background: #005296;
    border-radius: .4rem;
    word-break: break-all;
    margin-top: 8px;
    transition: opacity 0.4s;
}



.todo-text, .delete, .change {
    cursor: pointer;
}

.delete {
    margin-right: .5rem;
}

.completed {
    opacity: 0.2;
}

.row:nth-child(4n){
    background: linear-gradient(90deg,#005296,#3ca7ff)
}

.row:nth-child(4n + 1) {
    background: linear-gradient(90deg,#fca92c,#a60)
}

.row:nth-child(4n + 2) {
    background: linear-gradient(90deg,#00db63,#009945)
}

.row:nth-child(4n + 3) {
    background: linear-gradient(90deg,#b03aff,#8e03eb);
}
</style>