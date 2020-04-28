<template>
  <div>
    <v-container fluid>
      <v-data-iterator
        :items="items"
        :search="search"
        hide-default-footer
      >
        <template v-slot:header>
          <v-toolbar
            dark
            color="blue darken-3"
            class="mb-1"
          >
            <v-text-field
              v-model="search"
              clearable
              flat
              solo-inverted
              hide-details
              label="Search"
            />
          </v-toolbar>
        </template>
        <template v-slot:default="props">
          <v-row>
            <v-col
              v-for="item in props.items"
              :key="item.name"
              cols="12"
              sm="6"
              md="4"
              lg="3"
            >
              <v-card>
                <v-card-title class="subheading font-weight-bold">
                  {{ item.nombre }}
                </v-card-title>
                <v-img
                  src="https://placekitten.com/380/200"
                  height="194"
                />
                <v-divider />
                <v-list dense>
                  <v-list-item
                    v-for="(key, index) in filteredKeys"
                    :key="index"
                  >
                    <v-list-item-content :class="{ 'blue--text': sortBy === key }">
                      {{ key }}:
                    </v-list-item-content>
                    <v-list-item-content class="align-end" :class="{ 'blue--text': sortBy === key }">
                      {{ item[key.toLowerCase()] }}
                    </v-list-item-content>
                  </v-list-item>
                </v-list>
              </v-card>
            </v-col>
          </v-row>
        </template>
      </v-data-iterator>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'TheRecipePreview',
  data: () => ({
    filter: {},
    sortBy: 'nombre',
    keys: [
      'Nombre',
      'Category',
      'Ingredient',
      'Descripcion',
      'Weblink'
    ],
    items: [
      { nombre: 'chuletas', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'lasagna', category: 'italian', ingredient: 'beef', descripcion: 'esta es una receta de lasagna', weblink: 'enlace 2' },
      { nombre: 'huevos', category: 'breakfast', ingredient: 'eggs', descripcion: 'esta es una receta de huevos', weblink: 'enlace 3' },
      { nombre: 'general tao', category: 'chinese', ingredient: 'pork', descripcion: 'esta es una receta de general tao', weblink: 'enlace 4' }
    ],
    search: ''
  }),
  computed: {
    filteredKeys () {
      return this.keys.filter(key => key !== 'Name')
    }
  }
}
</script>

<style scoped>
.separacion{
  padding: 10px;
}
.card {display:inline-block;}
</style>
