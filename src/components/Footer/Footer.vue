<template>
  <footer>
    <ul class="navigation navigation_footer">
      <li
        class="navigation-link"
        v-for="(item, index) of nav"
        :key="index"
        @click="navigated(item)"
      >
        <h4>{{ item.title }}</h4>
      </li>
    </ul>
    <div class="footer__contacts">
      <a href="tel:+7(812)555-55-55"  class="footer__phone">
        +7 (812) 555-55-55
      </a>
      <h5 class="footer__adress">г. Санкт-Петербург, ул. Ефимова, 3</h5>
    </div>
  </footer>
</template>

<script>
import { NAVIGATION_LINKS } from '../../utils/consts'

export default {
  name: 'Footer',
  props: ['navigated'],
  data: function () {
    return {
      nav: NAVIGATION_LINKS
    }
  }
}
</script>

<style>
@import url("../../styles/footer.css");
</style>
