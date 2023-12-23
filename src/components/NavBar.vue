<template>
    <Disclosure as="nav" class="bg-gray-800" v-slot="{ open, close }">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="relative flex h-16 items-center justify-between">
          <div class="absolute inset-y-0 left-0 flex items-center md:hidden">
            <!-- Mobile menu button-->
            <DisclosureButton class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
              <span class="absolute -inset-0.5" />
              <span class="sr-only">Open main menu</span>
              <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
              <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
            </DisclosureButton>
          </div>
          <div class="flex flex-1 ml-14 sm:items-stretch sm:justify-start">
            <div class="flex flex-shrink-0 items-center">
              <RouterLink to="/">
                <img class="h-8 w-auto" src="https://www.mintyhost.com/wp-content/uploads/2023/06/mintyhost-logotipo.svg" alt="Your Company" />
              </RouterLink>
            </div>
            <div class="hidden sm:ml-6 md:block">
              <div class="flex space-x-4">
                <RouterLink v-for="item in navigation" :key="item.name" :to="item.to" :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'rounded-md px-3 py-2 text-sm font-medium']" :aria-current="item.current ? 'page' : undefined">{{ item.name }}</RouterLink>
              </div>
            </div>
          </div>
          <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">

            <!-- <button type="button" class="relative rounded-full bg-gray-800 p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-gray-800">
              <span class="absolute -inset-1.5" />
              <span class="sr-only">View notifications</span>
              <BellIcon class="h-6 w-6" aria-hidden="true" />
            </button> -->

            <!-- Language Selector -->
            <LanguageSelect />
          </div>
        </div>
      </div>
  
      <DisclosurePanel class="sm:hidden">
        <div class="space-y-1 px-2 pb-3 pt-2">
          <RouterLink 
            v-for="item in navigation" 
            :key="item.name" 
            :to="item.to" 
            :class="[route.path === item.to ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'block rounded-md px-3 py-2 text-base font-medium']"
            @click="close">
              {{ item.name }}
          </RouterLink>
        </div>
      </DisclosurePanel>
    </Disclosure>
  </template>
  
  <script setup>
    import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue'
    import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'
    import { useRoute } from 'vue-router'
    import LanguageSelect from './LanguageSelect.vue'
  
    const route = useRoute()
    
    const navigation = [
      { name: 'Viviendas', to: '/viviendas', current: false },
      { name: 'Preguntas', to: 'preguntas', current: false },
      { name: 'Contacto', to: '/contacto', current: false },
    ]

    const languages = [
      { name: 'es', src: "../assets/img/es.png" },
      { name: 'en', src: "../assets/img/en.png" },
      { name: 'fr', src: "../assets/img/fr.png" },
      { name: 'it', src: "../assets/img/it.png" },
      { name: 'de', src: "../assets/img/de.png" },
    ]
  </script>