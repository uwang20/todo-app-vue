<template>
  <div id="filter-stat">
      <div class="stat">
          <div class="completed">
              Completed: <span class="completed-value">{{todosStatus.completed}}</span>
          </div>
          <div class="remaining">
            Remainings: <span class="remaining-value">{{todosStatus.remainings}}</span>
          </div>
      </div>
      <div class="filter">
        <div class="filtered-option" @click="dropDown">
            <div class="selected-option">{{selectedOption}}</div>
            <div class="filter-down">
                <svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px"
                    width="14" height="14"
                    viewBox="0 0 172 172"
                    style=" fill:#000000;">
                    <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#41b883"><path d="M86,101.91827l57.98798,-56.79928c2.58413,-2.53246 6.71875,-2.50662 9.30288,0.05168l10.15565,10.15565c2.58413,2.60998 2.58413,6.79628 -0.02584,9.38041l-72.74339,72.27824c-1.29206,1.29207 -2.97175,1.9381 -4.67728,1.9381c-1.70553,0 -3.38522,-0.64603 -4.67728,-1.9381l-72.74339,-72.27824c-2.60997,-2.58413 -2.60997,-6.77043 -0.02584,-9.38041l10.15565,-10.15565c2.58413,-2.55829 6.71875,-2.58413 9.30288,-0.05168z"></path></g></g></svg>
            </div>
        </div>
        <div class="options-container">
            <div class="options" v-if="showOptions">
                <div @click="chosenFilter('all')" class="filter-option option-all">All</div>
                <div @click="chosenFilter('completed')" class="filter-option option-completed">Completed</div>
                <div @click="chosenFilter('remainings')" class="filter-option option-remainings">Remainings</div>
            </div>
        </div>
      </div>
  </div>

  
</template>

<script>
export default {
    name: 'FilterAndStat',
    props: {
        todosStatus: {
            type: Object,
            required: true
        }
    },
    data(){
        return {
            showOptions: false,
            selectedOption: 'All',
        }
    },
    methods: {
        dropDown(){
            this.showOptions = !this.showOptions
        },
        chosenFilter(filter){
            this.$emit('chosenFilter',filter)
            this.showOptions = !this.showOptions
            this.selectedOption = filter.charAt(0).toUpperCase() + filter.slice(1,filter.length)
        }
    }
}
</script>

<style scoped>
    #filter-stat{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 8px 14px;
    }

    .stat{
        display: flex;
        align-items: center;
        color: rgba(0,0,0,0.6)
    }

    .remaining{
        margin-left: 10px;
    }

/* Filter */

    .filter{
        width: 140px;
        min-width:100px;
        cursor: pointer;
    }

    .filtered-option{
        display: flex;
        align-items: center;
        justify-content: space-between;

        background-color: transparent;
        border: 2px solid #35495E;
    }

    .selected-option{
        padding: 3px 5px;
    }

    .filter-down{
        padding: 3px 8px;
        background-color: #35495E;
    }

    .options-container{
        position: relative;
    }

    .options{
        position: absolute;
        background-color: #FFFFFF;
        width: 100%;
        border: 2px solid #35495E;
        border-top: none;
    }

    .filter-option{
        padding: 3px 5px;
        transition: ease-in 0.2s;
        font-weight: 500;
        color: rgba(0,0,0,0.8);
    }

    .filter-option:hover{
        background-color: rgba(65, 184, 131,0.5);
    }
</style>