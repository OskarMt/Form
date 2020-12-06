<template>
  <div id="modal">
    <button id="show-modal__btn" @click="showModal = true" @mousedown="updateWindowWidth">Show Modal</button>

    <div class="modal-window" :class="{ show: showModal }">
      <form class="form" :class="{second:showSecondChapter}" @submit.prevent="checkForm">

        <!--FIRST-CHAPTER-->
        <section class="first-chapter">

          <!--HEADER-->

          <div class="header">
            <div class="header__title">Мой отзыв</div>
            <img src="@/assets/images/Union.png" class="header__close" @click="showModal = false, showTextError = false, commentary = '', showRatingError = false" @mousedown="clearRating"/>
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
          <div class="rating"  :class="{error:showRatingError}" @mouseout="checkStarRating">
            <div class="rating-item">
              <h3 class="rating-item__title">Скорость</h3>
              <stars ref="stars1"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Скорость отдачи видео</h3>
              <stars ref="stars2"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Качество</h3>
              <stars ref="stars3"></stars>
            </div>
            <div class="rating-item">
              <h3 class="rating-item__title">Пунктуальность</h3>
              <stars ref="stars4"></stars>
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
            <div class="album-imgs__img">
              <img class="album-imgs__img" src="@/assets/images/addImgBtn.png" alt="">
            </div>
            <div class="album-imgs__img">
              <div class="album-imgs__delete"><img src="@/assets/images/delete.png" alt=""></div>
              <img class="album-imgs__img" src="@/assets/images/albumImg1.jpg" alt="">
            </div>
            <div class="album-imgs__img">
              <div class="album-imgs__delete"><img src="@/assets/images/delete.png" alt=""></div>
              <img class="album-imgs__img" src="@/assets/images/albumImg2.jpg" alt="">
            </div>
            <div class="album-imgs__img">
              <div class="album-imgs__delete"><img src="@/assets/images/delete.png" alt=""></div>
              <img class="album-imgs__img" src="@/assets/images/albumImg3.jpg" alt="">
            </div>
            <div class="album-imgs__img">
              <div class="album-imgs__delete"><img src="@/assets/images/delete.png" alt=""></div>
              <img class="album-imgs__img" src="@/assets/images/albumImg4.jpg" alt="">
            </div>
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

    clearRating(){
      this.$refs.stars1.resetRating();
      this.$refs.stars2.resetRating();
      this.$refs.stars3.resetRating();
      this.$refs.stars4.resetRating();
    },

    /*Уведомление об ошибке*/
    showError(){
      this.showErrorAlert = true;
      setTimeout(()=>{
        this.showErrorAlert = false;
      }, 2000);
    },

    checkForm() {

      /*Валидация комментариев*/
      if(!this.commentary){
        this.showTextError = true;
        this.showError();

        /*Валидация звездного рейтинга*/
      }else if(this.$refs.stars1.getRating() == 0 || this.$refs.stars2.getRating() == 0 || this.$refs.stars3.getRating() == 0 || this.$refs.stars4.getRating() == 0){
        this.showRatingError = true
        this.showError();

      }else{
        this.showTextError = false;
        this.showRatingError = false;
        this.showModal = false;
        this.commentary = "";
        this.clearRating();

        this.showSuccessAlert = true;
        setTimeout(()=>{
          this.showSuccessAlert = false;
        }, 2000);
        return true
      }

    },

    /*Проверка блока комментариев при потере фокуса*/
    checkTextArea(){
      if(this.commentary){
        this.showTextError = false;
      }
    },

    /*Проверка звездного рейтинга при потере фокуса*/
    checkStarRating(){
      if(!(this.$refs.stars1.getRating() == 0 || this.$refs.stars2.getRating() == 0 || this.$refs.stars3.getRating() == 0 || this.$refs.stars4.getRating() == 0)){
        this.showRatingError = false;
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

  /*Счетчик символов в комментарии*/
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
