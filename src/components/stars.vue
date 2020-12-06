<template>
    <div class="stars">
       <span
       class="stars__item"
       v-for="rating in 5"
       :key="rating"
       @click="setRating(rating)"
       :class="{checked: updateRating(rating)}"
       @mouseover="updateHoverRating(rating)"
       @mouseout="returnSelectedRating"
>
            <star></star>
       </span>
    </div>
</template>


<script>
import star from "./starIcon"

export default{

    components:{
        star
    },

    data(){
        return{
            currentRating:0,
            hoverRating:0
        }
    },
    methods:{
      updateRating(n){
        return this.currentRating - n >= 0;
      },
      /*Обновление при клике*/
      setRating(n){
        this.currentRating = n;
        this.hoverRating = this.currentRating;

      },

      /*Обновление при ховере*/
      updateHoverRating(n){
        this.currentRating = n;
      },
      returnSelectedRating(){
        this.currentRating = this.hoverRating
      },

    }

}

</script>


<style>

  .stars__item{
    cursor: pointer;
    margin-right: 12.67px;
    fill:#EAECF0;
  }

  .stars__item:last-child{
    margin-right: 0;
  }

  .stars__item.checked{
    fill:#53C6D1;
  }



</style>
