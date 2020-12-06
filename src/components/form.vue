<template>
  <div id="modal">
    <button id="show-modal" @click="showModal = true" @mousedown="updateWindowWidth">Show Modal</button>

    <div class="modal-window" :class="{ show: showModal }">
      <form class="form" :class="{second:showSecondChapter}" @submit.prevent="checkForm">

        <!--FIRST-CHAPTER-->
        <section class="first-chapter">

          <!--HEADER-->

          <div class="header">
            <div class="header__title">Мой отзыв</div>
            <img src="@/assets/images/Union.png" class="header__close" @click="showModal = false, showTextError = false, commentary = '' "/>
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
          <div class="rating" :class="{error:showRatingError}">
            <div class="rating-item">
              <h3 class="rating-item__title">Скорость</h3>
              <stars ref="star1"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Скорость отдачи видео</h3>
              <stars ref="star2"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Качество</h3>
              <stars ref="star3"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Пунктуальность</h3>
              <stars ref="star4"></stars>
            </div>
          </div>

          <!--CONTINUE (max-width = 320px)-->
          <div class="continue" v-if="showChapterElem">
            <div class="continue__btn" @click="showSecondChapter = true">Продолжить</div>
          </div>
        </section>

       <!--SECOND-CHAPTER-->
        <section class="second-chapter">

          <!--HEADER (max-width = 320px)-->
          <div class="header mobile" v-if="showChapterElem">
            <div class="header-return">
              <img src="@/assets/images/arrow.png" class="header__arrow" @click="showSecondChapter = false"/>
              <div class="header__title">Мой отзыв</div>
            </div>
            <img src="@/assets/images/Union.png" class="header__close" @click="showModal = false, showTextError = false, commentary = '' "/>
          </div>


          <!--COMMENTARY-->
          <textarea type="text" maxlength="500" placeholder="Комментарий" class="commentary" :class="{error:showTextError}" @blur="checkTextArea" v-model="commentary"></textarea>
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
        </section>
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
      showTextError:false,
      showRatingError:false,

      showSecondChapter:false,
      showChapterElem: false,

      windowWidth:0
    }
  },
  components: {
      stars
  },
  methods:{
    checkForm() {

      /*Валидация блока комментариев*/
      if(this.commentary){
        this.showModal = false

        this.showSuccessAlert = true;
        this.commentary = ""
        setTimeout(()=>{
          this.showSuccessAlert = false;
        }, 2000);
        return true;
      }else{
        this.showTextError = true;

        this.showErrorAlert = true;
        setTimeout(()=>{
          this.showErrorAlert = false;
        }, 2000);
      }
    },
    checkTextArea(){
      if(this.commentary){
        this.showTextError = false;
      }
    },

    /*Определение размера экрана*/
    updateWindowWidth(){
      this.width = window.innerWidth;
      console.log(this.width)
      if(this.width <=640){
        this.showChapterElem = true
      }else{
        this.showChapterElem = false
      }
    }
  },
    created(){
      window.addEventListener('resize', this.updateWindowWidth);
    },
  computed:{
    letterCounter(){
      return this.commentary.length
    }
  }
}
</script>

<style lang="scss">
  @import '@/styles/style.scss';

</style>
