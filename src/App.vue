<template>
  <div id="app">
    <Header :filter="filter" :navigated="navigated" />
    <Main
      :items="filteredItems"
      :basket="basket"
      :addToBasket="addToBasket"
      :removeFromBasket="removeFromBasket"
      :addedToBasket="addedToBasket"
      :openPopup="openPopup"
    />
    <Footer :navigated="navigated" />
    <Popup
    :openedPopupData="openedPopupData"
    :closePopup="closePopup"
    />
  </div>
</template>

<script>
import Header from './components/Header/Header'
import Main from './components/Main/Main'
import Footer from './components/Footer/Footer'
import Popup from './components/Popup/Popup'

import { ITEMS } from './utils/consts'

export default {
  name: 'App',
  data: function () {
    return {
      items: ITEMS,
      filteredItems: ITEMS,
      basket: [],
      addedToBasket: [],
      openedPopupData: null
    }
  },
  components: {
    Header,
    Main,
    Footer,
    Popup
  },
  methods: {
    filter (arg) {
      const filtered = this.items.filter(item => {
        if (
          item.title.toLowerCase().includes(arg) ||
          item.price.includes(arg)
        ) {
          return item
        }
      })
      this.filteredItems = filtered
    },

    updateLocalStorage () {
      localStorage.setItem('items', JSON.stringify(this.basket))
    },

    addToBasket (id) {
      this.addedToBasket.push(id)
      setTimeout(() => {
        this.basket.push(id)
        this.updateLocalStorage()
      }, 1250)
    },

    removeFromBasket (id) {
      const removedIndex = this.addedToBasket.findIndex(item => item === id)
      const addedStart = this.basket.slice(0, removedIndex)
      const addedEnd = this.basket.slice(removedIndex + 1)
      this.addedToBasket = [...addedStart, ...addedEnd]
      setTimeout(() => {
        const basketIndex = this.basket.findIndex(item => item === id)
        const start = this.basket.slice(0, basketIndex)
        const end = this.basket.slice(basketIndex + 1)
        this.basket = [...start, ...end]
        this.updateLocalStorage()
      }, 1250)
    },

    getFromLocalStorage () {
      if (localStorage.getItem('items')) {
        this.basket = JSON.parse(localStorage.getItem('items'))
        this.addedToBasket = JSON.parse(localStorage.getItem('items'))
      }
    },

    openPopup (e, id) {
      if (!e.target.classList.contains('item__price-button')) {
        const index = ITEMS.findIndex(item => item.id === id)
        if (ITEMS[index].enabled) {
          this.openedPopupData = ITEMS[index]
        }
      }
    },

    closePopup () {
      this.openedPopupData = null
    },

    navigated (item) {
      if (item.link) {
        window.location.replace(`${window.location.origin}/${item.link}`)
      } else {
        alert('Страница находится на реконструкции. Приносим свои извинения.')
      }
    }
  },

  mounted () {
    this.getFromLocalStorage()
  }
}
</script>

<style>
@import url("../normalize.css");
@import url("../styles.css");
</style>
