<template>
  <div id="app">
    <product-list-component></product-list-component>
  </div>
</template>

<script>
import ProductListComponent from './components/products/ProductListComponent'

export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    ProductListComponent
  }
}
</script>

<style>
</style>
