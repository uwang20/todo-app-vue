<template>
  <div id="add-todos-modal" @click="closeModal">
        <div class="back-x" id="back-to-main">
          X
        </div>
        <transition name="fade">
             <div class="add-todos" v-show="openAddModal">
          <div class="add-todos-nav">
              <div>
                  <h1 id="add-todos-label">ADD TODOS</h1>
              </div>
              <div>
                  <svg @click="createTodo" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                    width="30" height="30"
                    viewBox="0 0 172 172"
                    style=" fill:#000000;">
                    <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M86,1.24038c-46.79868,0 -84.75962,37.96094 -84.75962,84.75962c0,46.79868 37.96094,84.75962 84.75962,84.75962c46.79868,0 84.75962,-37.96094 84.75962,-84.75962c0,-46.79868 -37.96094,-84.75962 -84.75962,-84.75962zM130.55048,59.77103l-45.45493,67.03246c-1.34375,1.98978 -3.48858,3.33353 -5.60757,3.33353c-2.11899,0 -4.44471,-1.16286 -5.94351,-2.63581l-26.66827,-26.69412c-1.8089,-1.80889 -1.8089,-4.78065 0,-6.58954l6.58954,-6.58954c1.8089,-1.8089 4.78065,-1.8089 6.56371,0l17.36538,17.33954l37.72837,-55.66226c1.44712,-2.11899 4.36719,-2.66166 6.48618,-1.24038l7.72656,5.24579c2.09315,1.42128 2.66166,4.34135 1.21454,6.46033z"></path></g></g></svg>
              </div>
          </div>
          <div class="add-todos-body">
                <div class="set-title-form">
                    <input :class="{'no-title':hasNoTitle}" @keydown.enter="addTitle" @blur="addTitle"  type="text" class="title-textbox" placeholder="title here...">
                </div>
                <div class="add-todos-form">
                    <div class="todo-here">Todos here... </div>
                    <svg @click="addForm" id="add-form-icon" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                        width="35" height="35"
                        viewBox="0 0 172 172"
                        style=" fill:#000000;">
                        <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M141.04,13.76h-110.08c-9.4944,0 -17.2,7.7056 -17.2,17.2v110.08c0,9.4944 7.7056,17.2 17.2,17.2h110.08c9.4944,0 17.2,-7.7056 17.2,-17.2v-110.08c0,-9.4944 -7.7056,-17.2 -17.2,-17.2zM127.28,89.44h-37.84v37.84h-6.88v-37.84h-37.84v-6.88h37.84v-37.84h6.88v37.84h37.84z"></path></g></g></svg>
                </div>
              <div class="todo-forms">
                  <div v-for="(form, index) in todoFormArray" :key='index' class="todo-form">
                    <input type="text" @keydown.enter="finishTodo" @focus="getIndex(index)" class="todo-textbox" v-model="todoForm[index]">
                    <div class="delete-todo-form">
                        <svg @click="deleteForm(index)" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 229.103 229.103"><path fill="#41B883" d="M80.679,162a16,16,0,0,1-16-16V97.321H16a16,16,0,0,1-16-16v-.643a16,16,0,0,1,16-16H64.679V16a16,16,0,0,1,16-16h.643a16,16,0,0,1,16,16V64.679H146a16,16,0,0,1,16,16v.643a16,16,0,0,1-16,16H97.321V146a16,16,0,0,1-16,16Z" transform="translate(114.551) rotate(45)"/></svg>
                    </div>
                  </div>
              </div>
          </div>
      </div>
        </transition>
  </div>
</template>

<script>
export default {
    name: 'AddTodosModal',
    props: {
        todoFormArray: {
            type: Array,
            required: true
        },
        todoForm: {
            type: Array,
            required: true
        },
        hasNoTitle: {
            type: Boolean,
            required: true
        },
        openAddModal: {
            type: Boolean,
            required: true
        }
    },
    data(){
        return {
            todosTitle: '',
            textBoxIndex: 0,
            hasTitle: this.hasNoTitle
        }
    },
    methods: {
        addToTodosArray(event){
           this.$emit('addToTodosArray',event)
        },
        editTodos(index){
           this.$emit('editTodos',index)
        },
        addForm(){
            let todoForm = document.querySelector('.todo-forms')
            this.$emit('addForm',todoForm)

        },
        deleteForm(index){
            this.$emit('deleteForm',index)
        },
        addTitle(event){
            let todoForm = document.querySelector('.todo-forms')
            this.$emit('addTitle',event, todoForm)
        },
        finishTodo(event){
            let todoForm = document.querySelector('.todo-forms')
            this.$emit('finishForm')
            this.$emit('finishTodo',event,todoForm)
        },
        getIndex(index){
            this.$emit('getIndex',index)
        },
        createTodo(){
            let noTitleForm = document.querySelector('.title-textbox')
            noTitleForm.value = ''
            this.$emit('createTodo',noTitleForm)
        },
        closeModal(event){
            this.$emit('closeModal',event)
        }
    }
}
</script>

<style scoped>
    #add-todos-modal{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        background-color: rgba(0,0,0,0.5);
        backdrop-filter: blur(5px);
    }

    #add-todos-label{
        color: rgba(255,255,255,0.5);
    }

    .back-x{
        position: absolute;
        top: 0;
        right: 0;
        margin: 10px;
    }

    #add-form-icon{
        transition: 0.2s ease-in
    }

    #add-form-icon:active{
        transform: scale(1.1)
    }

    .no-title{
        background-color: rgba(255, 0, 0,0.1);
    }

    .add-todos{
        width: 550px;
        margin: 0 auto;
        margin-top: 50px;

        background-color: #FFFFFF;

        border-radius: 10px;
    }

    .add-todos-nav{
        display: flex;
        align-items: center;
        justify-content: space-between;

        background-color: #35495E;
        padding: 22px 25px 40px 25px;

        border-radius: 10px 10px 0 0;
    }

    .add-todos-body{
        padding: 40px 15px 15px 15px;
        font-size: 1.4rem;
    }

    .set-title-form{
        display: flex;
        margin-bottom: 15px;
    }

    .title-textbox{
        flex: 1;
        height: 2.2rem;
        font-size: 1.2rem;
        padding-left: 3px;

        outline: none;
        border: none;
        border-bottom: 1px solid #41B883;
    }

    .add-todos-form{
        display: flex;
        align-items: center;
        justify-content: space-between;

        margin-bottom: 15px;
    }

    .todo-here{
        font-size: 1.2rem;
        color: rgba(0,0,0,0.5);
    }

    .todo-form{
        display: flex;
        align-items: center;
        justify-content: space-between;

        margin-bottom: 10px;
    }

    .todo-textbox{
        flex:1;
        height: 2rem;
        font-size: 1.2rem;
        padding-left: 3px;

        border: none;
        border-bottom: 1px solid #41B883;
    }

    .delete-todo-form{
        margin-left: 5px;
    }

    .fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>