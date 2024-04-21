<template>
  <div class="v-catalog">
    <div><h1>catalog</h1></div>
    <div class="v-catalog_list">
      <vCatalogItem
        v-for="product in PRODUCTS"
        :key="product.article"
        v-bind:product_data="product"
        @addToCard="addToCard"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from './v-catalog-item.vue'
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'v-catalog',
  components: { vCatalogItem },
  props: {},
  data () {
    return {}
  },
  computed: {
    ...mapGetters(['PRODUCTS'])
  },
  methods: {
    ...mapActions(['GET_PRODUCTS_FROM_API', 'ADD_TO_CARD']),
    addToCard (data) {
      this.ADD_TO_CARD(data)
    }
  },
  mounted () {
    this.GET_PRODUCTS_FROM_API()
      .then((response) => {
        if (response.data) {
          console.log('Данные пришли')
        }
      })
  }
}
</script>

<style>
.v-catalog,
.v-catalog_list {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
}
</style>
