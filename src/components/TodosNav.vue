<template>
  <div id="todos-nav">
    <div class="todo-title">
        <div>
            <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                v-if="!todoList.areAllCompleted"
                @click="checkAll(todoListIndex)"
                width="22" height="22"
                viewBox="0 0 172 172"
                style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M139.75,13.23077c10.49159,0 19.01923,8.52765 19.01923,19.01923v107.5c0,10.49159 -8.52764,19.01923 -19.01923,19.01923h-107.5c-10.49158,0 -19.01923,-8.52764 -19.01923,-19.01923v-107.5c0,-10.49158 8.52765,-19.01923 19.01923,-19.01923h107.5M139.75,0h-107.5c-17.80469,0 -32.25,14.44531 -32.25,32.25v107.5c0,17.80469 14.44531,32.25 32.25,32.25h107.5c17.80469,0 32.25,-14.44531 32.25,-32.25v-107.5c0,-17.80469 -14.44531,-32.25 -32.25,-32.25z"></path></g></g></svg>
            <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                v-else
                @click="checkAll(todoListIndex)"
                width="22" height="22"
                viewBox="0 0 172 172"
                style=" fill:#000000;"><g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M32.25,0c-17.80469,0 -32.25,14.44531 -32.25,32.25v107.5c0,17.80469 14.44531,32.25 32.25,32.25h107.5c17.80469,0 32.25,-14.44531 32.25,-32.25v-107.5c0,-17.80469 -14.41947,-32.25 -32.25,-32.25zM32.25,13.23077h107.5c10.49159,0 19.01923,8.52765 19.01923,19.01923v107.5c0,10.49159 -8.52764,19.01923 -19.01923,19.01923h-107.5c-10.49158,0 -19.01923,-8.52764 -19.01923,-19.01923v-107.5c0,-10.49158 8.52765,-19.01923 19.01923,-19.01923zM126.93269,30.59615c-1.60216,0.3101 -3.15264,1.24038 -4.13462,2.6875l-51.68269,76.28365l-23.98077,-23.77404c-2.48077,-2.48077 -6.38281,-2.48077 -8.88942,0l-9.09615,9.09615c-2.50661,2.48077 -2.50661,6.61538 0,9.09615l36.59135,36.59135c2.06731,2.04147 5.375,3.51442 8.26923,3.51442c2.89423,0 5.76262,-1.80889 7.64904,-4.54808l62.22596,-91.78846c1.98978,-2.89423 1.26622,-6.92548 -1.65385,-8.88942l-10.54327,-7.23558c-1.44712,-0.98197 -3.15264,-1.34375 -4.75481,-1.03365z"></path></g></g></svg>
        </div>
        <div class="title-date">
            {{todoList.todosTitle}}
            <span class="date">{{todoList.dateCreated}}</span>
        </div>
    </div>
    <div class="btn-back" @click="backToTodoLists()">BACK</div>
  </div>
</template>

<script>
export default {
    name: 'TodosNav',
    props: {
        todoList: {
            type: Object,
            required: true
        },
        todoListIndex: {
            type: Number,
            required: true
        }
    },
    methods: {
        backToTodoLists(){
            this.$emit('backToTodoLists')
        },
        checkAll(todoListIndex){
            this.$emit('checkAll',todoListIndex)
        }
    }
}
</script>

<style>
    #todos-nav {
        display: flex;
        align-items: center;
        justify-content: space-between;

        padding: 14px 20px;
    }

    .todo-title{
        display: flex;
        align-items: center;
    }

    .title-date{
        font-size: 2rem;

        margin-left: 10px;
    }

    .date{
        font-size: 1rem;

        margin-left: 5px;

        color: rgba(0,0,0,0.5)
    }

    .btn-back{
        padding: 6px 16px;
        background-color: #35495E;
        border-radius: 8px;

        transition: ease-in 0.3s;
        cursor: pointer;

        color: #FFFFFF;
    }
    .btn-back:hover{
        border-radius: 0;
        background-color: rgba(53, 73, 94,0.8);
    }
</style>