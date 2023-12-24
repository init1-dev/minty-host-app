<template>
    <div class="card" @click="open = true">
        <img :src="apartment.pic[0]" class="mb-2 img" alt="imagen de la propiedad">
        <h1>{{ apartment.apartment_title }}</h1>
        <p>Barrio {{ apartment.barrio.name }}</p>
        <p>{{ apartment.square_meter }}m2</p>
        <p>{{ apartment.bedrooms }} habitaciones</p>
        <p>{{ apartment.monthly_price }}€/mes</p>
        <p class="mt-3 text-center border border-black rounded ver-mas">Click para ver más detalles</p>
    </div>

    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
        <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
        </TransitionChild>
  
        <div class="fixed inset-0 z-10 w-screen overflow-y-auto mt-14 sm:mt-0">
          <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
            <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
              <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
                <div class="bg-white px-4 pb-4 pt-5 sm:p-6 sm:pb-4">
                  <!-- Modal -->
                  <div class="sm:flex sm:items-start">
                    <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                      <div class="mt-2">
                        <!-- Cuerpo del modal -->
                        <!-- <img v-for="(pic, i) in apartment.pic" :key=i :src=pic class="mb-2 img" alt="imagen de la propiedad"> -->

                        <vueper-slides fade class="mb-3" fixed-height="500px">
                            <vueper-slide
                                v-for="(pic, i) in apartment.pic" 
                                :key=i 
                                :image=pic
                                alt="imagen de la propiedad">
                            </vueper-slide>
                        </vueper-slides>

                        <h1>{{ apartment.apartment_title }}</h1>
                        <p>{{ apartment.address }}</p>
                        <p>{{ apartment.town }}</p>
                        <p>Barrio {{ apartment.barrio.name }}</p>
                        <p>{{ apartment.square_meter }}m2</p>
                        <p>{{ apartment.bedrooms }} habitaciones</p>
                        <p>{{ apartment.monthly_price }}€/mes</p>

                        <DialogTitle as="h3" class="mt-5 text-base font-semibold leading-6 text-gray-900">Equipamiento:</DialogTitle>
                        <!-- Iconos -->
                        <div class="iconos">
                            <!-- Wifi -->
                            <div class="icon-box">
                                <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full sm:mx-0 sm:h-10 sm:w-10">
                                    <WifiIcon class="h-6 w-6 text-black-600" aria-hidden="true" />
                                </div>
                                <p>Wifi: 
                                    <b v-if="apartment.amenities.wifi">Sí</b>
                                    <b v-else>No</b>
                                </p>
                            </div>
                            <!-- Aire acondicionado -->
                            <div class="icon-box">
                                <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full sm:mx-0 sm:h-10 sm:w-10">
                                    <DeviceTabletIcon class="h-6 w-6 text-black-600" aria-hidden="true" />
                                </div>
                                <p>A/C: 
                                    <b v-if="apartment.amenities['A/C']">Sí</b>
                                    <b v-else>No</b>
                                </p>
                            </div>
                            <!-- Calefacción -->
                            <div class="icon-box">
                                <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full sm:mx-0 sm:h-10 sm:w-10">
                                    <SunIcon class="h-6 w-6 text-black-600" aria-hidden="true" />
                                </div>
                                <p>Calefacción: 
                                    <b v-if="apartment.amenities.heating">Sí</b>
                                    <b v-else>No</b>
                                </p>
                            </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="bg-gray-50 px-4 py-3 sm:flex sm:flex-row-reverse sm:px-6">
                    <button type="button" class="inline-flex w-full justify-center rounded-md bg-blue-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-500 sm:ml-3 sm:w-auto" @click="open = false">Comprobar disponibilidad</button>
                    <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto" @click="open = false" ref="cancelButtonRef">Cerrar</button>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
</template>

<script setup>
    import { ref } from 'vue'
    import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
    import { WifiIcon, DeviceTabletIcon, SunIcon } from "@heroicons/vue/24/solid"

    import { VueperSlides, VueperSlide } from 'vueperslides'
    import 'vueperslides/dist/vueperslides.css'

    const open = ref(false)

    const slides = [
        {
            title: 'Slide #1',
            content: 'Slide 1 content.'
        },
        {
            title: 'Slide #2',
            content: 'Slide 2 content.'
        }
    ]
</script>

<script>
    export default {
        props: {
            apartment: {
                type: Object,
                required: true
            }
        }
    };
</script>

<style>
  .ver-mas {
    margin-top: auto;
    color: black;
    font-weight: 500;
    background-color: lightgreen;
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
    min-height: 400px;
  }

  .card .img {
    border: 1px solid grey;
  }
  
  .card:hover {
    transform: translateY(-0.3rem);
    box-shadow: 0.5rem 0.5rem 0.5rem #aaa;
  }

  .iconos {
    display: flex;
    align-items: center;
  }

  .icon-box {
    margin-top: 0.5rem;
    margin-right: 0.5rem;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    border: 1px solid lightgray;
    padding: 0 0.5rem 0 0.5rem;
  }
</style>

<!-- Ejemplo de objeto de la respuesta de la API:
{
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