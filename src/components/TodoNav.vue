<template>
  <div id="todo-nav">
      <div class="title-container">
          <h1>TO - VUE</h1>
          <h4>Just do it!</h4>
      </div>
      <div class="add-btn-container">
          <svg @click="openAddTodoModal" id="add-icon" xmlns="http://www.w3.org/2000/svg" width="35" height="35" viewBox="0 0 168 168"><path fill="#41b883" d="M84,168a83.607,83.607,0,0,1-46.965-14.346A84.246,84.246,0,0,1,6.6,116.7a83.889,83.889,0,0,1,7.745-79.662A84.246,84.246,0,0,1,51.3,6.6a83.89,83.89,0,0,1,79.662,7.745A84.245,84.245,0,0,1,161.4,51.3a83.89,83.89,0,0,1-7.745,79.662A84.245,84.245,0,0,1,116.7,161.4,83.475,83.475,0,0,1,84,168ZM38.085,71.915a11.586,11.586,0,0,0,0,23.171H72.414v34.329a11.586,11.586,0,1,0,23.171,0V95.086h34.329a11.586,11.586,0,0,0,0-23.171H95.585V37.586a11.586,11.586,0,0,0-23.171,0V71.915Z"/></svg>
      </div>
  </div>
</template>

<script>
export default {
    name: 'TodoNav',
    methods: {
        openAddTodoModal(){
            this.$emit('openAddTodoModal')
        }
    }
}
</script>

<style scoped>
#todo-nav{
    display: flex;
    align-items: center;
    justify-content: space-between;

    background-color: #35495E;
    color: #BEE3F8;

    padding: 2rem 1rem;

    border-radius: 16px 16px 0 0;
}

.add-btn-container{
    margin-right: 10px;
}

#add-icon{
    transition: 0.3s ease-in;
}

#add-icon:hover{
    transform: scale(1.1);
}

</style>