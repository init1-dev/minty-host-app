<template>
  
  <div>
    <div class="filters-grid mt-5">
      <div class="text-center mr-2">
        <label for="filter">Filtrar por: </label>
        <select id="filter" class="filters" v-model="selectedFilter">
            <option value="todos">Todos</option>
            <option v-for="filter in filters" :key="filter.id" :value="filter.id">{{ filter.name }}</option>
        </select>
      </div>
      <button class="filtros-btn" @click="applyFilter">enviar</button>
    </div>
    <h1 class="mt-5 mb-3 text-center">Resultados de la búsqueda</h1>
    <div class="card-container mb-5 ml-5 mr-5">
      <div v-if="searchResult" class="card-container mb-5 ml-5 mr-5">
        <!-- Tarjetas de las propiedades -->
        <div v-for="property in searchResult" :key="property.id" class="card">
          <img :src="property.pic[0]" class="mb-2 img" alt="imagen de la propiedad">
          <h1>{{ property.apartment_title }}</h1>
          <p>{{ property.address }}</p>
          <p>Barrio {{ property.barrio.name }}</p>
          <p>{{ property.square_meter }}m2</p>
          <p>{{ property.bedrooms }} habitaciones</p>
          <p>{{ property.monthly_price }}€/mes</p>
          <p class="mt-3 text-center border border-black rounded ver-mas">Click para ver más detalles</p>
          <!-- Otros datos relevantes de la propiedad -->
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

export default {
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

  .card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    padding: 10px;
    width: 300px;
    background-color: #e2e2e2;
    color:black;
    border-radius: 0.5rem;
    min-width: 300px;
    box-shadow: 0.1rem 0.1rem 0.1rem #aaa;
    transition: all 0.5s;
    overflow: hidden;
    min-height: 420px;
  }

  .card .img {
    border: 1px solid grey;
  }

  .ver-mas {
    margin-top: auto;
    color: black;
    font-weight: 500;
    background-color: lightgreen;
  }
  
  .card:hover {
    transform: translateY(-0.3rem);
    box-shadow: 0.5rem 0.5rem 0.5rem #aaa;
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
</style>

<!-- {
  "id": 1,
  "address": "Calle Gran Vía, 123, Madrid",
  "apartment_title": "Luminoso apartamento en Malasaña",
  "monthly_price": 3000,
  "accommodates_max": 4,
  "barrio": {
    "id": 1,
    "name": "Malasaña"
  },
  "square_meter": 100,
  "bedrooms": 3,
  "bathrooms": 2,
  "amenities": {
    "wifi": true,
    "A/C": true,
    "heating": false
  },
  "pic": [
    "https://myplazze-contents.s3.eu-west-1.amazonaws.com/apartments/apartment_544/photos/637913972541774829.jpg",
    "https://myplazze-contents.s3.eu-west-1.amazonaws.com/apartments/apartment_1529/photos/FPJhs9uxv6W8qNgJewDbVWNHXoQqHLCa.jpg",
    "https://myplazze-contents.s3.eu-west-1.amazonaws.com/apartments/apartment_1529/photos/bYCtJCsK9jhi35Hkl5puJ21AP32LwbYO.jpg",
    "https://myplazze-contents.s3.eu-west-1.amazonaws.com/apartments/apartment_1529/photos/yEe14DYFPxRBdhevWbu7s2KqjGmTu96W.jpg"
  ],
  "town": "Madrid"
}, -->