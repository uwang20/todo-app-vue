<template>
    <div>
        <div id="todo-list"
            @mouseover="showCount()" 
            @mouseleave="dontShowCount()"
             > 
            <div class="todo-list-title" @click="showTodos(index)">
                <div class="title-count">
                    {{todoList.todosTitle}}
                    <span   v-show="showTodosCount" 
                            class="todos-count">({{todoList.todos.length}} todos)</span>
                </div>
                <div class="todo-list-date">
                    {{todoList.dateCreated}}
                </div>
            </div>
            <div class="todo-list-delete">
                <svg @click="deleteTodoList(index)" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 229.103 229.103">
                    <path fill="#41B883" d="M80.679,162a16,16,0,0,1-16-16V97.321H16a16,16,0,0,1-16-16v-.643a16,16,0,0,1,16-16H64.679V16a16,16,0,0,1,16-16h.643a16,16,0,0,1,16,16V64.679H146a16,16,0,0,1,16,16v.643a16,16,0,0,1-16,16H97.321V146a16,16,0,0,1-16,16Z" transform="translate(114.551) rotate(45)"/>
                </svg>
            </div>
        </div>
    </div>    
</template>

<script>
export default {
    name: 'TodoList',
    props: {
        todoList: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    data(){
        return {
            showTodosCount: false
        }
    },
    methods: {
        showCount(){
            this.showTodosCount = true
        },
        dontShowCount(){
            this.showTodosCount = false
        },
        showTodos(index){
            this.$emit('showTodos',index)
        },
        deleteTodoList(index){
            this.$emit('deleteTodoList',index)
        }
    }
}
</script>

<style scoped>
#todo-list{
    display: flex;
    align-items: center;

    transition: ease-in 0.2s;

    padding: 10px 15px;

    font-size: 1.6rem;
}

#todo-list:hover{
    background-color: rgba(65, 184, 131, 0.1);
}

.todo-list-title{
    flex: 1;
}

.title-count{
    display: flex;
    align-items: center;

    margin-bottom: 5px;
}

.todos-count{
    font-size: 1rem;
    margin-left: 10px;

    color: rgba(0,0,0,0.4);

    transition: ease-in 0.3s;
}

.todo-list-date{
    font-size: 0.9rem;
    margin-left: 5px;

    color: rgba(0,0,0,0.5);
}

</style>