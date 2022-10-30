<template>
  <section v-if="openedPopupData !== null" class="popup popup_opened">
    <article class="popup__container">
      <img
        :src="closeIcon"
        class="popup__close"
        alt="закрыть"
        @click="closePopup"
      />
      <h2 class="popup__title">{{ openedPopupData.title }}</h2>
      <h2 class="popup__description">{{ openedPopupData.description }}</h2>
      <div class="popup__price-container">
        <h2 v-if="openedPopupData.oldPrice !== ''" class="popup__oldPrice">
          {{ openedPopupData.oldPrice }}
        </h2>
        <h2 class="popup__price">{{ openedPopupData.price }}</h2>
      </div>
      <div class="popup__slider">
        <div class="popup__slider-wrapper">
          <img
            :src="arrow"
            alt="предыдущий слайд"
            class="popup__slider-button"
            @click="swapSlide(false)"
          />
          <div
            :style="{
              backgroundImage: `url(${openedPopupData.src})`,
              backgroundPositionX: posX,
              backgroundPositionY: posY,
              backgroundSize: size,
              transitionProperty: tProp
            }"
            class="popup__slide"
          >
            <div class="popup__controller-listener">
              <div class="popup__controller">
                <div
                  v-for="(item, index) of openedPopupData.slider"
                  :key="index"
                  @click="toCurrentSlide(item, index)"
                  :class="
                    index === slideCounter
                      ? 'popup__controller-button popup__controller-button_active'
                      : 'popup__controller-button'
                  "
                ></div>
              </div>
            </div>
          </div>
          <img
            :src="arrow"
            alt="следующий слайд"
            class="popup__slider-button popup__slider-button_next"
            @click="swapSlide(true)"
          />
        </div>
        <div class="popup__slider-icons"></div>
      </div>
    </article>
  </section>
  <section v-else class="popup"></section>
</template>

<script>
import * as closeIcon from '../../assets/icons/close.svg'
import * as arrow from '../../assets/icons/arrow.svg'

export default {
  props: ['openedPopupData', 'closePopup'],
  data: function () {
    return {
      closeIcon: closeIcon,
      slideCounter: 0,
      arrow: arrow,
      posX: this.openedPopupData
        ? this.openedPopupData.slider[0].posX
        : 'center',
      posY: this.openedPopupData
        ? this.openedPopupData.slider[0].posY
        : 'center',
      size: this.openedPopupData
        ? this.openedPopupData.slider[0].size
        : 'contain',
      tProp: 'all'
    }
  },
  name: 'Popup',
  methods: {
    swapSlide (arg) {
      if (arg) {
        if (this.slideCounter < this.openedPopupData.slider.length - 1) {
          this.slideCounter++
          this.tProp = 'all'
        } else {
          this.tProp = 'none'
          this.slideCounter = 0
        }
      } else {
        if (this.slideCounter > 0) {
          if (this.slideCounter === 1) {
            this.tProp = 'none'
          }
          this.slideCounter--
        } else {
          this.tProp = 'all'
          this.slideCounter = this.openedPopupData.slider.length - 1
        }
      }
      this.posX = this.openedPopupData.slider[this.slideCounter].posX
      this.posY = this.openedPopupData.slider[this.slideCounter].posY
      this.size = this.openedPopupData.slider[this.slideCounter].size
    },

    toCurrentSlide (item, index) {
      if (index === 0) {
        this.tProp = 'none'
      } else {
        this.tProp = 'all'
      }
      this.slideCounter = index
      this.posX = item.posX
      this.posY = item.posY
      this.size = item.size
    }
  }
}
</script>

<style scoped>
@import url("../../styles/popup.css");
</style>
