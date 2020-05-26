<template>
    <div id="todos-body">
        <div v-for="(todo,index) in todosFilter" :key="todo.key" id="todo" class="todos-instance">
            <div class="todo-checkbox">
                <div class="checkbox">
                    <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                        v-show="!todo.isCompleted"
                        @click="checkTodo(index,todoListIndex)"
                        width="22" height="22"
                        viewBox="0 0 172 172"
                        style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M139.75,13.23077c10.49159,0 19.01923,8.52765 19.01923,19.01923v107.5c0,10.49159 -8.52764,19.01923 -19.01923,19.01923h-107.5c-10.49158,0 -19.01923,-8.52764 -19.01923,-19.01923v-107.5c0,-10.49158 8.52765,-19.01923 19.01923,-19.01923h107.5M139.75,0h-107.5c-17.80469,0 -32.25,14.44531 -32.25,32.25v107.5c0,17.80469 14.44531,32.25 32.25,32.25h107.5c17.80469,0 32.25,-14.44531 32.25,-32.25v-107.5c0,-17.80469 -14.44531,-32.25 -32.25,-32.25z"></path></g></g></svg>
                    <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                        v-show="todo.isCompleted"
                        @click="checkTodo(index,todoListIndex)"
                        width="22" height="22"
                        viewBox="0 0 172 172"
                        style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M32.25,0c-17.80469,0 -32.25,14.44531 -32.25,32.25v107.5c0,17.80469 14.44531,32.25 32.25,32.25h107.5c17.80469,0 32.25,-14.44531 32.25,-32.25v-107.5c0,-17.80469 -14.41947,-32.25 -32.25,-32.25zM32.25,13.23077h107.5c10.49159,0 19.01923,8.52765 19.01923,19.01923v107.5c0,10.49159 -8.52764,19.01923 -19.01923,19.01923h-107.5c-10.49158,0 -19.01923,-8.52764 -19.01923,-19.01923v-107.5c0,-10.49158 8.52765,-19.01923 19.01923,-19.01923zM126.93269,30.59615c-1.60216,0.3101 -3.15264,1.24038 -4.13462,2.6875l-51.68269,76.28365l-23.98077,-23.77404c-2.48077,-2.48077 -6.38281,-2.48077 -8.88942,0l-9.09615,9.09615c-2.50661,2.48077 -2.50661,6.61538 0,9.09615l36.59135,36.59135c2.06731,2.04147 5.375,3.51442 8.26923,3.51442c2.89423,0 5.76262,-1.80889 7.64904,-4.54808l62.22596,-91.78846c1.98978,-2.89423 1.26622,-6.92548 -1.65385,-8.88942l-10.54327,-7.23558c-1.44712,-0.98197 -3.15264,-1.34375 -4.75481,-1.03365z"></path></g></g></svg>
                </div>  
                <div class="todo-text-edit">
                    <div v-show="!todo.showEdit">{{todo.name}}</div> 
                    <input @keydown.enter="updateTodo(index)" v-show="todo.showEdit" type="text" class="text-edit" v-model="todo.name">
                </div>
            </div>
            <div>
                <div class="edit-delete">
                    <div class="edit">
                        <svg  @click="showEdit(index)" v-show="!todo.showEdit" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                                width="20" height="20"
                                viewBox="0 0 172 172"
                                style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g id="original-icon" fill="#41b883"><path d="M131.96744,14.33333c-1.83376,0 -3.66956,0.69853 -5.06706,2.09961l-12.23372,12.23372l28.66667,28.66667l12.23372,-12.23372c2.80217,-2.80217 2.80217,-7.33911 0,-10.13412l-18.53255,-18.53255c-1.40108,-1.40108 -3.23329,-2.09961 -5.06706,-2.09961zM103.91667,39.41667l-82.41667,82.41667v28.66667h28.66667l82.41667,-82.41667z"></path></g></g></svg>
                        
                        <div @click="updateTodo(index)" v-show="todo.showEdit" id="save">save</div>
                    </div>
                    <div class="delete">
                        <svg @click="deleteTodo(index)" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 229.103 229.103"><path fill="#41B883" d="M80.679,162a16,16,0,0,1-16-16V97.321H16a16,16,0,0,1-16-16v-.643a16,16,0,0,1,16-16H64.679V16a16,16,0,0,1,16-16h.643a16,16,0,0,1,16,16V64.679H146a16,16,0,0,1,16,16v.643a16,16,0,0,1-16,16H97.321V146a16,16,0,0,1-16,16Z" transform="translate(114.551) rotate(45)"/></svg>
                    </div>
                </div>
            </div>    
        </div>
    </div>
</template>

<script>
export default {
    name: 'Todo',
    props: {
        todoListIndex: {
            type: Number,
            required: true
        },
        todoLists:{
            type: Array,
            required: true
        },
        todosFilter: {
            type: Array,
            required: true
        }
    },
    methods: {
        checkTodo(index,todoListIndex){
            this.$emit('checkTodo',index,todoListIndex)
        },
        showEdit(index){
            let todoEdit = document.querySelector('.todos-instance').parentNode.children[index].children[0].children[1].children[1]
            this.$emit('showEdit',index, todoEdit)
        },
        updateTodo(index){
            this.$emit('updateTodo',index)
        },
        deleteTodo(index){
            this.$emit('deleteTodo',index)
        }
    }
}
</script>

<style scoped>
#todo{
    display: flex;
    align-items: center;
    justify-content: space-between;

    padding: 8px 20px;

    transition: ease 0.2s;
}

#todos-body{
    overflow-y: scroll;
    height: 275px;
}

#todo:hover{
    background-color: rgba(65, 184, 131,0.2);
}

.todo-checkbox{
    display: flex;
    align-items: center;
}

.checkbox{
    margin-right: 10px;
}

.edit-delete{ 
    display: flex;
    align-items: center;
}

#save{
    color: #41B883;
    font-weight: 700;
    cursor: pointer;
}

.edit{
    margin-right: 8px;
}

.todo-text-edit{
    font-size: 1.4rem;
} 

.text-edit{
    font-size: 1.4rem;
    outline: none;
    border: none;
    padding:2px;
    padding-left: 4px;
    border: 1px solid #41B883;
    border-radius: 5px;
}

::-webkit-scrollbar-thumb{
    background-color: rgba(65, 184, 131,0.5);
}

::-webkit-scrollbar{
    background-color: transparent;
    width: 10px;
}
</style>