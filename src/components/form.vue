<template>
  <div id="modal">
    <button id="show-modal" @click="showModal = true">Show Modal</button>

    <div class="modal-window" :class="{ show: showModal }">
      <form class="form" @submit="checkForm">

       <!--HEADER-->
        <div class="header">
          <div class="header__title">Мой отзыв</div>
          <img src="@/assets/images/Union.png" class="header__close" @click="showModal = false"/>
        </div>

        <!--ALBUM-->
        <div class="album">
          <img src="@/assets/images/wedding.jpg" alt="" class="album__photo">
          <div class="album-text">
            <h2 class="album-text__title">Фоточки в свадебном платьице</h2>
            <p class="album-text__owner">Алена Смирнова</p>
          </div>
        </div>

        <!--RATING-->
        <div class="rating">
          <div class="rating-item">
            <h3 class="rating-item__title">Скорость</h3>
            <stars></stars>
          </div>
          <div class="rating-item">
            <h3 class="rating-item__title">Скорость отдачи видео</h3>
            <stars></stars>
          </div>
          <div class="rating-item">
            <h3 class="rating-item__title">Качество</h3>
            <stars></stars>
          </div>
          <div class="rating-item">
            <h3 class="rating-item__title">Пунктуальность</h3>
            <stars></stars>
          </div>
        </div>

        <!--COMMENTARY-->
        <textarea type="text" maxlength="500" placeholder="Комментарий" class="commentary" v-model="commentary"></textarea>
        <div class="commentary-counter">{{ letterCounter }}/500</div>

        <!--ALBUM-IMGS-->
        <div class="album-imgs">
          <img class="album-imgs__img" src="@/assets/images/addImgBtn.png" alt="">
          <img class="album-imgs__img" src="@/assets/images/albumImg1.jpg" alt="">
          <img class="album-imgs__img" src="@/assets/images/albumImg2.jpg" alt="">
          <img class="album-imgs__img" src="@/assets/images/albumImg3.jpg" alt="">
          <img class="album-imgs__img" src="@/assets/images/albumImg4.jpg" alt="">
        </div>

        <!--FOOTER-->
        <div class="footer">
          <input class="footer__btn" type="submit" value="Отправить">
        </div>

        <p v-if="errors.length">
          <b>Пожалуйста заполните необходимые поля</b>
          <ul>
            <li v-for="error in errors" :key="error">{{ error }}</li>
          </ul>
        </p>

        <p class="alert">Спасибо, отзыв опубликован!</p>


      </form>
    </div><!--/MODAL-WINDOW-->
  </div><!--//MODAL-->
</template>

<script>

import stars from "./stars"

export default {
  name: 'App',
  data(){
    return{
      showModal:false,
      commentary:"",
      errors:[],
    }
  },
  components: {
      stars
  },
  methods:{
    checkForm: function(e) {
      if(this.commentary){
        return true;
      }

      this.errors = [];

      if(!this.commentary){
        this.errors.push('Напишите комментарий.');
      }

      e.preventDefault();
    },

  },
  computed:{
      letterCounter: function(){
      return this.commentary.length
    }

  }
}
</script>

<style lang="scss">
  @import '@/styles/style.scss';

</style>
