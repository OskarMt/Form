<template>
    <div class="stars">
       <span class="stars__item" v-for="star in ratings" :key="star">
            <star :iconColor="color"></star>
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
            ratings: [1,2,3,4,5],
            color: "#EAECF0",
            temp_value:null
        }
    },
    methods:{

    }
}


</script>


<style>

    .stars__item{
        cursor: pointer;
        margin-right: 12.67px;
    }
    .stars__item:last-child{
        margin-right: 0;
    }


</style>
