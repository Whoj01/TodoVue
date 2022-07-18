<template>
    <div class="modal-wrapper" >
            <div class="modal">
                <h2>Edite o texto</h2>
                <input type="text" v-model="textoToPatch">
                   <div class="buttons">
                       <button  @click="sendingInformations" class="change">Mudar</button>
                       <button @click="cancelChange" class="cancel" >cancelar</button>
                   </div>
            </div>
        </div>
</template>

<script>


export default {
    props: {
        show: Boolean,
        patchTodo: Object
    },
    data(){
        return{
            showLocal: this.show,
            textoToPatch: this.patchTodo.texto,
            patchTodoLocal: this.patchTodo
        }
    },
    methods: {
        sendingInformations(){
            
            if(this.textoToPatch !== ''){
                  this.patchTodoLocal.texto = this.textoToPatch
                  this.$emit('patchedText', this.patchTodoLocal)
                  this.showLocal = false
                  this.$emit('closeModal', this.showLocal)
            } else {
                   this.showLocal = false
                   this.$emit('closeModal', this.showLocal)  
            }     
        },
        cancelChange(){
            this.showLocal = false
            this.$emit('closeModal', this.showLocal)
        },
    },

   
    
}
</script>


<style>
.modal-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1000;
    width: 100vw;
    height: 100vh;
    color: #1b1b1b;
    background: rgba(4, 9, 17, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
}

.modal {
    width: min(59rem, 90%);
    background: #ffff;
    margin: auto;
    padding: 2rem 4rem;
    border-radius: 6px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    
}

input {
    outline: none;
    width: 70%;
    padding: .5rem;
    font-size: .8rem;
    border: 2px solid #005296;
    background: transparent;
    border-radius: .4rem;
    color: #1b1b1b;
    margin-bottom: 1rem;
    
}

.buttons button{
    border: none;
    padding: 1rem;
    border-radius: 8px;
    font-size: .8rem;
    cursor: pointer;
    font-weight: 700;
    color: #ffff;
    transition: filter 2;
}

.buttons button.change{
    margin-right: 2rem;
    background: linear-gradient(90deg,#005296,#3ca7ff);
}

.buttons button.cancel {
  background: linear-gradient(90deg, #F94C66, #B25068);
}

.buttons button:hover {
  filter: brightness(.8);
}
</style>