<template>
  <div id="modal">
    <button id="show-modal" @click="showModal = true">Show Modal</button>

    <div class="modal-window" :class="{ show: showModal }">
      <form class="form" @submit.prevent="checkForm">

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
        <textarea type="text" maxlength="500" placeholder="Комментарий" class="commentary" :class="{error:showError}" v-model="commentary"></textarea>
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
          <input class="footer__btn" type="submit" value="Отправить" >
        </div>

      </form>
    </div><!--/MODAL-WINDOW-->

    <!--ALERT-->
    <p class="alert-submit" :class="{active:showSuccessAlert}">Спасибо, отзыв опубликован!</p>
    <p class="alert-error" :class="{active:showErrorAlert}">Заполните необходимые поля</p>


  </div><!--/MODAL-->
</template>

<script>

import stars from "./stars"

export default {
  name: 'App',
  data(){
    return{
      showModal:false,
      commentary:"",
      showSuccessAlert:false,
      showErrorAlert:false,
      showError:false
    }
  },
  components: {
      stars
  },
  methods:{
    checkForm: function() {

      /*Валидация блока комментариев*/
      if(this.commentary){
        this.showModal = false
        this.showSuccessAlert = true;
        setTimeout(()=>{
          this.showSuccessAlert = false;
        }, 2000);
        return true;
      }else{
        this.showError = true;
        this.showErrorAlert = true;
        setTimeout(()=>{
          this.showErrorAlert = false;
        }, 2000);
      }
    }


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
