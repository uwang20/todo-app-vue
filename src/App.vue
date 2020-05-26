<template>
  <div id="app">
    <div id="todo-app">
      <TodoNav @openAddTodoModal='openAddTodoModal'></TodoNav>
      <div class="todo-lists-body" v-if="!areTodosOpen">
          <TodoList v-for="(todoList,index) in todoLists"
                    @showTodos='showTodos'
                    :todoList="todoList" 
                    :index="index"
                    :key="todoList.key"
                    @deleteTodoList='deleteTodoList'
                    ></TodoList>
      </div>
      <div class="todos-body" v-else>
        <TodosNav @checkAll='checkAll' @backToTodoLists='backToTodoLists' :todoList="todoLists[todoListIndex]" :todoListIndex="todoListIndex"></TodosNav>
        <FilterAndStat :todosStatus="todosStatus" @chosenFilter="chosenFilter"></FilterAndStat>
        <Todo :todoListIndex="todoListIndex" :todoLists="todoLists" @deleteTodo='deleteTodo' @showEdit='showEdit' @updateTodo='updateTodo' @checkTodo="checkTodo" :todosFilter="todosFilter"></Todo>
      </div>
    </div>
    <AddTodosModal  v-show='openAddModal'
                    @addForm='addForm'
                    @deleteForm='deleteForm'
                    @finishTodo='finishTodo'
                    @getIndex='getIndex'
                    @finishForm='finishForm'
                    @createTodo='createTodo'
                    @closeModal='closeModal'
                    :todoFormArray="todoFormArray"
                    :todoForm="todoForm"
                    :hasNoTitle="hasNoTitle"
                    :openAddModal="openAddModal"
                    @addTitle="addTitle"></AddTodosModal>
   <DeleteConfirmationModal v-show="openDeleteModal"
                            @deleteThis='deleteThis'
                            @dontDelete='dontDelete'></DeleteConfirmationModal>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import Todo from './components/Todo.vue'
import TodoNav from './components/TodoNav.vue'
import TodosNav from './components/TodosNav.vue'
import FilterAndStat from './components/FilterAndStat.vue'
import AddTodosModal from './components/AddTodosModal.vue'
import DeleteConfirmationModal from './components/DeleteConfirmationModal.vue'

export default {
  name: 'App',
  components: {
    TodoList,
    TodoNav,
    Todo,
    TodosNav,
    FilterAndStat,
    AddTodosModal,
    DeleteConfirmationModal
  },
  data() {
    return {
      todoLists: [
        {
          todosTitle: 'Title 1',
          areAllCompleted: false,
          dateCreated: 'Dec 20, 2020',
          key: 1,
          todos: [
            {
              name: 'hello form title 1',
              isCompleted: false,
              showEdit: false,
              key: 1
            },
            {
              name: 'hi  there from title 1',
              isCompleted: false,
              showEdit: false,
              key: 2
            },
            {
              name: 'yowz from title 1',
              isCompleted: false,
              showEdit: false,
              key: 3
            }
          ]
        },
        {
          todosTitle: 'Title 2',
          areAllCompleted: false,
          dateCreated: 'Dec 20, 2020',
          key: 2,
          todos: [
            {
              name: 'todo 2',
              isCompleted: false,
              showEdit: false,
              key: 1
            },
            {
              name: 'todo 2',
              isCompleted: false,
              showEdit: false,
              key: 2
            }
          ]
        }
      ],
      areTodosOpen: false,
      todoListIndex: undefined,
      filter: 'all',
      todoFormArray: [''],
      todoForm: [],
      todosTitle: '',
      textBoxIndex: undefined,
      todoKey: 3,
      todoListKey: 3,
      hasNoTitle: false,
      openAddModal: false,
      editTodoCache: '',
      openDeleteModal: false,
      todoListIndexToDelete: undefined,
      todoIndexToDelete: undefined
    }
  },
  methods: {
    showTodos(index){
      // console.log(event.target.id) 
      // console.log(index)
      // if(event.target.id === 'delete-todoLists') return
      this.todoListIndex = index
      this.areTodosOpen = true 
    },
    backToTodoLists(){
      this.areTodosOpen = false
      this.filter = 'all'
    },
    checkTodo(index,todoListIndex){
      if(this.filter==='completed' || this.filter==='remainings') return
      this.todoLists[todoListIndex].todos[index].isCompleted = !this.todoLists[todoListIndex].todos[index].isCompleted
      
      let allCompleted = this.todoLists[todoListIndex].todos.every(todo => todo.isCompleted)

      if(allCompleted){
        this.todoLists[todoListIndex].areAllCompleted = true
      }
      else{
        this.todoLists[todoListIndex].areAllCompleted = false
      }

      if(this.filter === 'completed'){
        return this.todoLists[this.todoListIndex].todos.filter(todo => {
              return todo.isCompleted
          }) 
      }
    },
    checkAll(todoListIndex){
      if(this.filter==='completed' || this.filter==='remainings') return
      this.todoLists[todoListIndex].areAllCompleted = !this.todoLists[todoListIndex].areAllCompleted
      
      if(this.todoLists[todoListIndex].areAllCompleted){
        this.todoLists[todoListIndex].todos.forEach(todo => {
          todo.isCompleted = true
        })
      }
      else{
        this.todoLists[todoListIndex].todos.forEach(todo => {
          todo.isCompleted = false
        })
      }
    },
    chosenFilter(filter){
      this.filter = filter
    },
    addForm(todoForm){
      // if(this.textBoxIndex === undefined) this.textBoxIndex = 0
      if(this.todoFormArray.length > 9) return
      this.todoFormArray.push('')
      console.log(this.todoFormArray.length)
      setTimeout(() => {
        todoForm.children[this.todoFormArray.length-1].children[0].focus()
      },100)
      // this.textBoxIndex++
      
    },
    deleteForm(index){
      this.todoFormArray.splice(index,1)
      this.todoForm.splice(index,1)
      this.textBoxIndex--
    },
    addTitle(event,todoForm){
      if(this.todosTitle !== '') this.hasNoTitle = false
      this.todosTitle = event.target.value
      event.target.blur()
      if(this.todoFormArray.length === 0) this.todoFormArray.push('')
      setTimeout(() => {
        todoForm.children[0].children[0].focus()
      },100)

      // console.log(title)
    },
    finishTodo(event,todoForm){
      event.target.blur()
      setTimeout(() => {
       if(this.todoFormArray.length < 11){
         todoForm.children[this.textBoxIndex+1].children[0].focus()
         if(this.todoFormArray.length === 10) this.textBoxIndex--
       } 
      },100) 
    },
    finishForm(){
      if(this.textBoxIndex !== this.todoFormArray.length-1) return
      if(this.todoFormArray.length > 9) return 
      this.todoFormArray.push('')
    },
    getIndex(index){
      this.textBoxIndex = index
    },
    createTodo(noTitleForm){
      if(this.todosTitle === ''){
        noTitleForm.focus()
        return this.hasNoTitle = true
      } 
      let todos = []

      this.todoForm = this.todoForm.filter(todo => {
        return todo != undefined
      })

      this.todoForm.forEach(todo => {
          todos.push({
            name: todo,
            isCompleted: false,
            showEdit: false,
            key: this.todoKey++
        })
      })

      this.todoLists.push({
        todosTitle: this.todosTitle,
        areAllCompleted: false,
        dateCreated: 'date',
        key: this.todoListKey++,
        todos: todos
      })

      this.openAddModal = false
      this.todoForm = []
      this.todoFormArray = ['']
      this.todosTitle = ''
      this.todoKey = 3
      this.textBoxIndex = undefined


      console.log(this.todosTitle)
      console.log(this.todoLists)
      
      // console.log(this.todoForm)
      // console.log(this.todosTitle)
      // console.log(typeof this.todoForm[1])
    },
    openAddTodoModal(){
      this.openAddModal = true
    },
    closeModal(event){
      if(event.target.id === 'add-todos-modal' || event.target.id === 'back-to-main') this.openAddModal = false
    },
    showEdit(index,todoEdit){
      console.log(this.todoLists[this.todoListIndex].todos[index].name)
      this.editTodoCache = this.todoLists[this.todoListIndex].todos[index].name
      setTimeout(() => {
        todoEdit.focus()
      },100)
      this.todoLists[this.todoListIndex].todos[index].showEdit = !this.todoLists[this.todoListIndex].todos[index].showEdit
    },
    updateTodo(index){
        let todo = this.todoLists[this.todoListIndex].todos[index].name
        if(todo === '' || todo.length === 0) this.todoLists[this.todoListIndex].todos[index].name = this.editTodoCache
        this.todoLists[this.todoListIndex].todos[index].showEdit = !this.todoLists[this.todoListIndex].todos[index].showEdit
        console.log(this.todoLists[this.todoListIndex].todos[index].name)
    },
    deleteTodoList(index){
      this.todoListIndexToDelete = index
      this.openDeleteModal = true
    },
    deleteTodo(index){
      this.todoIndexToDelete = index
      this.openDeleteModal = true
    },
    deleteThis(){
        if(this.todoListIndexToDelete >= 0){
          this.todoLists.splice(this.todoListIndexToDelete,1)
          this.todoListIndexToDelete = undefined
        }
        if(this.todoIndexToDelete >= 0){
          this.todoLists[this.todoListIndex].todos.splice(this.todoIndexToDelete,1)
          this.todoIndexToDelete = undefined
        }
        this.openDeleteModal = false
    },
    dontDelete(){
      this.openDeleteModal = false
      this.todoListIndexToDelete = undefined
      this.todoIndexToDelete = undefined
    }
  },
  computed: {
    todosStatus(){
      let totalTodos = this.todoLists[this.todoListIndex].todos.length
      let status = {
        completed: 0,
        remainings: totalTodos
      }
      this.todoLists[this.todoListIndex].todos.forEach(todo => {
        if(todo.isCompleted) status.completed++
      })

      status.remainings = totalTodos - status.completed

      return status
    },
    todosFilter(){
      if(this.filter === 'completed'){
          return this.todoLists[this.todoListIndex].todos.filter(todo => {
                      return todo.isCompleted == true
                  }) 
      }
      else if(this.filter === 'remainings'){
          return this.todoLists[this.todoListIndex].todos.filter(todo => {
                      return todo.isCompleted == false
                  })
      }
      else{
          return this.todoLists[this.todoListIndex].todos
      } 

    }
  }
}
</script>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

body{
 background-color: #41B883;;
}

#todo-app{
  width: 650px;
  height: 525px;

  margin: 0 auto;
  margin-top: 75px;

  background-color: #FFFFFF;

  border-radius: 16px; 
}

.todo-lists-body{
  margin-top: 10px;
  overflow-y: scroll;
  height: 375px;
}

::-webkit-scrollbar-thumb{
    background-color: rgba(65, 184, 131,0.5);
}

::-webkit-scrollbar{
    background-color: transparent;
    width: 10px;
}
</style>
