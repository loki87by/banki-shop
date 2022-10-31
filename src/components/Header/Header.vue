<template>
  <header>
    <ul class="navigation">
      <li
        class="navigation-link"
        v-for="(item, index) of nav"
        :key="index"
        @click="navigated(item)"
      >
        <h4>{{ item.title }}</h4>
      </li>
    </ul>
    <div class="header__search">
      <input
        type="text"
        class="header__searchInput"
        :placeholder="width > 320 ? 'Поиск по названию картины' : 'Поиск'"
        @input="filterItems"
      />
      <button type="button" @click="filterItems">Найти</button>
    </div>
  </header>
</template>

<script>
import { debounce } from '../../utils/helpers'
import { NAVIGATION_LINKS } from '../../utils/consts'

export default {
  name: 'Header',
  props: ['filter', 'navigated', 'width'],
  data: function () {
    return {
      inputed: '',
      nav: NAVIGATION_LINKS
    }
  },
  methods: {
    filterItems (e) {
      const text = e.target.value
      this.inputed = text
      debounce(this.filter, 1000, text)
    },

    filterFromButton () {
      this.filter(this.inputed)
    }
  }
}
</script>

<style>
@import url("../../styles/header.css");
</style>
