<template>
  <div>
    <SearchBar />
    <Propstest
      prp="String test result"
      :numero="numberProp"
      :stringoso="palabra"
      :objetos="recipes"
      :datoPadre="midato"
      v-on:ninoapadre="clicknino"
      v-on:aumento="contador++"
    />
    <p> {{ delnino }} </p>
    <TheRecipePreview />
  </div>
</template>

<script>
// import Propstest from './Propstest.vue'
import TheRecipePreview from './TheRecipePreview.vue'
// import SearchBar from '@/components/visitors/general/SearchBar'

export default {
  name: 'TheBody',
  components: {
    TheRecipePreview
    // SearchBar,
    // Propstest
  },
  data: () => ({
    numberProp: 666,
    palabra: 'test de variable string',
    recipes: [
      { id: '0', title: 'chuletas', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { id: '1', title: 'lasagna', category: 'italian', ingredient: 'beef', descripcion: 'esta es una receta de lasagna', weblink: 'enlace 2' },
      { id: '2', title: 'huevos', category: 'breakfast', ingredient: 'eggs', descripcion: 'esta es una receta de huevos', weblink: 'enlace 3' },
      { id: '3', title: 'general tao', category: 'chinese', ingredient: 'pork', descripcion: 'esta es una receta de general tao', weblink: 'enlace 4' }
    ],
    contador: 0,
    delnino: ''
  }),
  methods: {
    clicknino (value) {
      this.delnino = value
    }
  }
}
</script>

<style scoped>
</style>
