<template>
  <div class="housesPage">
    <div class="container">
      <div class="row flex-grow-1">
        <div class="col-md-4 my-3" v-for="h in houses">
          <HouseCard :house="h" />
        </div>

      </div>
      
    </div>


  </div>
</template>


<script>
import { onMounted, computed } from "vue";
import { AppState } from "../AppState.js";
import { housesService } from "../services/HousesService.js";
import Pop from "../utils/Pop.js";

export default {
  setup(){
    async function getHouses(){
      try {
        await housesService.getHouses()
      } catch (error) {
        Pop.error(error, 'getting homes')
      }
    }

    onMounted(()=>{
      getHouses()
    })
    
    return {
      account: computed(()=> AppState.account),
      houses: computed(()=> AppState.houses)
    }
  }
}
</script>


<style lang="scss" scoped>

</style>

