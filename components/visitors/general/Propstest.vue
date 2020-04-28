<template>
  <div>
    <p>String prop test: {{ prp }} </p>
    <p>Number prop test: {{ numero }} </p>
    <p>String variable prop test: {{ stringoso }}</p>
    <div v-for="objeto in objetos" :key="objeto.id">
      <p>
        Object prop test: {{ objeto.category }}
      </p>
    </div>
    <b-form-select v-model="selected" :options="options" />
    <b-button
      type="button"
      name="button"
      v-on:click="$emit('aumento')"
    >
      Prueba de props al revez
    </b-button>
    <label for="nino-input">Child input: </label>
    <b-form-input
      id="nino-input"
      type="text"
      name="msg"
      v-model="mensajeNino"
      v-on:keyup="mandarPadre"
    />
  </div>
</template>

<script>

export default {
  name: 'Propstest',
  components: {
  },
  props: {
    prp: String,
    numero: Number,
    stringoso: String,
    objetos: Array
  },
  data: () => ({
    selected: null,
    mensajeNino: ''
  }),
  methods: {
    mandarPadre (event) {
      this.$emit('ninoapadre', this.mensajeNino)
    }
  }
}
</script>

<style scoped>
</style>
