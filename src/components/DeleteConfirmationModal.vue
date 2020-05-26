<template>
  <div id="delete-confirmation-modal">
      <div class="confirmation">
          <div class="are-you-sure">
            <span>Are you sure?</span>
          </div>
          <div class="options">
            <span @click="deleteThis" id="yes">Yes</span>
            <span @click="dontDelete" id="no">No</span>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'DeleteConfirmationModal',
    methods: {
        deleteThis(){
            this.$emit('deleteThis')
        },
        dontDelete(){
            this.$emit('dontDelete')
        }
    }

}
</script>

<style scoped>
    #delete-confirmation-modal{
        width: 100%;
        height: 100vh;
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(0,0,0,0.5);
        backdrop-filter: blur(5px);
    }

    .confirmation{
        border-radius: 12px;
        padding: 30px 30px;

        width: 375px;
        margin: 0 auto;
        margin-top: 100px;
        background-color: #FFFFFF;
        text-align: center;
    }

    .are-you-sure{
        font-size: 1.6rem;
        margin-bottom: 15px;
        color: rgba(0,0,0,0.6);
    }

    .options{
        font-size: 1.3rem;
        font-weight: bold;
        cursor: pointer
    }

    #yes{
        margin-right: 15px;
    }
    #no{
        margin-left: 15px;
    }

    #yes:hover, #no:hover{
        color: #35495E;
    }
</style>