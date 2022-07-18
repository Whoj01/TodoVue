<template>
     <form @submit.prevent="send" >
                <input type="text" v-model="insert">
                <button type="submit">Adicionar</button>
            </form>
</template>

<script>

export default {

    data(){
        return{
            insert: '',
            
            newTodo: {}   
        }
    },
    methods: {
        send(){
            const id = this.todoList.length + 1
            if(this.insert !== ''){
                   this.newTodo = ({id: id, texto: this.insert, completed: false})
                   this.$emit('novoTodo', this.newTodo)
            }
            this.insert = ''
        }
    },
    props: {
        todoList: {
            type: Array,
            required: true
        }
    },
}
</script>

<style>
form {
    display: flex;
    margin-bottom: 2rem;
    width: 60%;
    justify-content: center;
    align-items: center;
}

form input {
    outline: none;
    width: 70%;
    padding: .5rem;
    font-size: .8rem;
    border: 2px solid #005296;
    background: transparent;
    border-radius: .4rem 0 0 .4rem;
    color: #ffff;
}

form button {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: calc(.5rem + 2.2px);
    border: none;
    font-size: .8rem;
    font-weight: 600;
    color: #ffff;
    background: linear-gradient(90deg,#005296,#3ca7ff);
    border-radius: 0 .4rem .4rem 0;
    width: 30%;
    cursor: pointer;
    margin-bottom: 15.9px;
}   
</style>