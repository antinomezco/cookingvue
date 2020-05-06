<template>
  <div>
    <v-container fluid>
      <v-data-iterator
        :items="recipes"
        :search="search"
        :items-per-page.sync="itemsPerPage"
        item-key="nombre"
        :single-expand="true"
        :sort-by="sortBy.toLowerCase()"
        :sort-desc="sortDesc"
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
            ></v-text-field>
            <template v-if="$vuetify.breakpoint.mdAndUp">
              <v-spacer></v-spacer>
              <v-btn-toggle
                v-model="sortDesc"
                mandatory
              >
                <v-btn
                  large
                  depressed
                  color="blue"
                  :value="false"
                >
                  <v-icon>mdi-arrow-up</v-icon>
                </v-btn>
                <v-btn
                  large
                  color="blue"
                  :value="true"
                >
                  <v-icon>mdi-arrow-down</v-icon>
                </v-btn>
              </v-btn-toggle>
            </template>
          </v-toolbar>
        </template>
        <template v-slot:default="{ items, isExpanded, expand }">
          <v-row>
            <v-col
              v-for="item in items"
              :key="item.nombre"
              cols="12"
              sm="6"
              md="4"
              lg="3"
            >
              <v-card>
                <v-card-title class="subheading font-weight-bold">
                  {{ item.nombre }}
                </v-card-title>
                <v-switch
                  :input-value="isExpanded(item)"
                  :label="isExpanded(item) ? 'Expanded' : 'Closed'"
                  class="pl-4 mt-0"
                  @change="(v) => expand(item, v)"
                ></v-switch>
                <v-img
                  src="https://placekitten.com/380/200"
                  height="194"
                />
                <v-divider></v-divider>
                <v-list v-if="isExpanded(item)" dense>
                  <v-list-item
                    v-for="(key, index) in filteredKeys"
                    :key="index"
                  >
                    <v-list-item-content :class="{ 'blue--text': sortBy === key }">{{ key }}:</v-list-item-content>
                    <v-list-item-content class="align-end" :class="{ 'blue--text': sortBy === key }">{{ item[key.toLowerCase()] }}</v-list-item-content>
                  </v-list-item>
                </v-list>
              </v-card>
            </v-col>
          </v-row>
        </template>
        <template v-slot:footer>
          <v-row class="mt-2" align="center" justify="center">
            <span class="grey--text">Items per page</span>
            <v-menu offset-y>
              <template v-slot:activator="{ on }">
                <v-btn
                  dark
                  color="primary"
                  class="ml-2"
                  v-on="on"
                >
                  {{ itemsPerPage }}
                  <v-icon>mdi-chevron-down</v-icon>
                </v-btn>
              </template>
              <v-list>
                <v-list-item
                  v-for="(number, index) in itemsPerPageArray"
                  :key="index"
                  @click="updateItemsPerPage(number)"
                >
                  <v-list-item-title>{{ number }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
            <v-spacer></v-spacer>
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
    // expand: false,
    itemsPerPageArray: [4, 8, 12],
    sortDesc: false,
    itemsPerPage: 4,
    filter: {},
    sortBy: 'nombre',
    keys: [
      'Nombre',
      'Category',
      'Ingredient',
      'Descripcion',
      'Weblink'
    ],
    recipes: [
      { nombre: 'chuletas', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'lasagna', category: 'italian', ingredient: 'beef', descripcion: 'esta es una receta de lasagna', weblink: 'enlace 2' },
      { nombre: 'huevos', category: 'breakfast', ingredient: 'eggs', descripcion: 'esta es una receta de huevos', weblink: 'enlace 3' },
      { nombre: 'general tao', category: 'chinese', ingredient: 'pork', descripcion: 'esta es una receta de general tao', weblink: 'enlace 4' },
      { nombre: 'banana', category: 'fruit', ingredient: 'banana', descripcion: 'es un platano', weblink: 'enlace 5' },
      { nombre: 'dulces', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'chancla', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'basura', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'cama', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'cobija', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'zoo', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'nalgas', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'arte', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'refresco', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' },
      { nombre: 'sandwich', category: 'american', ingredient: 'pork', descripcion: 'esta es una receta de chuletas', weblink: 'enlace 1' }
    ],
    search: ''
  }),
  computed: {
    filteredKeys () {
      return this.keys.filter(key => key !== 'Nombre')
    }
  },
  methods: {
    updateItemsPerPage (number) {
      this.itemsPerPage = number
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
