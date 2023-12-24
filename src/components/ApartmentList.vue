<template>
  <div>
    <!-- Filtros -->
    <div class="filters-grid mt-5 sm:mt-5">
      <div class="text-center mr-2">
        <label for="filter">Filtrar por: </label>
        <select id="filter" class="filters" v-model="selectedFilter">
            <option value="todos">Todos</option>
            <option v-for="filter in filters" :key="filter.id" :value="filter.id">{{ filter.name }}</option>
        </select>
      </div>
      <button class="filtros-btn" @click="applyFilter">Buscar</button>
    </div>
    <!-- Resultados de la busqueda -->
    <h1 class="mt-5 mb-3 text-center">Resultados de la búsqueda</h1>
    <!-- Contenedor de cards de las propiedades -->
    <div class="card-container mb-5 ml-5 mr-5">
      <div v-if="searchResult" class="card-container mb-5 ml-5 mr-5">
        <!-- Listado de propiedades -->
        <div v-for="property in searchResult" :key="property.id">
          <ApartmentCard :apartment="property"/>
        </div>
      </div>
      <div v-else class="mt-5 mb-5">
        <img src="../assets/img/loader.svg" alt="loader">
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import ApartmentCard from './ApartmentCard.vue'

  export default {
    components: {
      ApartmentCard
    },
    data() {
      return {
        searchResult: null,
        filters: null,
        selectedFilter: "todos"
      };
    },
    mounted() {
      // Llamada a la API al montar el componente
      this.performSearch();
      this.getFilters();
    },
    methods: {
      async performSearch() {
        try {
          // Realizar la llamada a la API usando Axios
          const response = await axios.post('https://api.dev.myplazze.com/api/v1/practice/search', {
            headers: {
              'Accept': 'application/json',
              'Content-Type': 'application/json'
            },
          });

          // Actualizar el estado con los datos recibidos
          this.searchResult = response.data;
        } catch (error) {
          console.error('Error al realizar la búsqueda:', error);
        }
      },
      async applyFilter() {
        if (this.selectedFilter == "todos") {
          this.performSearch()
        } else {
          let barrio = {
            "barrio_id": this.selectedFilter
          }
          try {
            // Realizar la llamada a la API usando Axios
            const response = await axios.post('https://api.dev.myplazze.com/api/v1/practice/search', barrio, {
              filter: this.selectedFilter,
              headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
              }
            });
    
            // Actualizar el estado con los datos recibidos
            this.searchResult = response.data;
          } catch (error) {
            console.error('Error al realizar la búsqueda:', error);
          }
        }

      },
      async getFilters() {
        try {
          // Realizar la llamada a la API usando Axios
          const response = await axios.get('https://api.dev.myplazze.com/api/v1/practice/barrios', {
            headers: {
              'Accept': 'application/json',
              'Content-Type': 'application/json'
            },
          });

          // Actualizar el estado con los datos recibidos
          this.filters = response.data;
        } catch (error) {
          console.error('Error al realizar la búsqueda:', error);
        }
      }
    }  
  };
</script>

<style>
  .card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: center;
    align-items: center;
  }

  h1 {
    font-weight: 800;
  }

  .filters {
    border-radius: 0.5rem;
  }
  .filters-grid {
    display: flex;
    justify-content: center;
  }
  .filtros-btn {
    padding: 0.5rem;
    background-color: lightseagreen;
    border-radius: 0.5rem;
    color: black;
    font-weight: 500;
  }

  @media (max-width: 1900px) {
    .filters-grid {
      margin-top: 0;
      top: 0;
    }
    .viviendas {
      padding-top: 0;
    }
  }
</style>