<template>
    <Listbox as="div" v-model="selected">
      <div class="relative">
        <ListboxButton class="relative w-full cursor-default rounded-md bg-white py-1.5 pl-2 pr-8 text-left text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 sm:text-sm sm:leading-6">
          <span class="flex items-center">
            <img :src="selected.src" :alt="selected.name" class="h-5 w-5 flex-shrink-0 rounded-full" />
            <span class="ml-1 block truncate">{{ selected.name }}</span>
          </span>
          <span class="pointer-events-none absolute inset-y-0 right-0 ml-3 flex items-center pr-2">
            <ChevronUpDownIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
          </span>
        </ListboxButton>
  
        <transition leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100" leave-to-class="opacity-0">
          <ListboxOptions class="absolute z-10 mt-1 max-h-56 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm">
            <ListboxOption as="template" v-for="item in languages" :key="item.id" :value="item" v-slot="{ active, selected }">
              <li :class="[active ? 'bg-indigo-600 text-white' : 'text-gray-900', 'relative cursor-default select-none py-2 pl-3 pr-9']">
                <div class="flex items-center">
                  <img :src="item.src" :alt="item.name" class="h-5 w-5 flex-shrink-0 rounded-full" />
                  <!-- <span :class="[selected ? 'font-semibold' : 'font-normal', 'ml-1 block truncate']">{{ item.name }}</span> -->
                </div>
  
                <span v-if="selected" :class="[active ? 'text-white' : 'text-indigo-600', 'absolute inset-y-0 right-0 flex items-center pr-4']">
                  <CheckIcon class="h-5 w-5" aria-hidden="true" />
                </span>
              </li>
            </ListboxOption>
          </ListboxOptions>
        </transition>
      </div>
    </Listbox>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import { Listbox, ListboxButton, ListboxOption, ListboxOptions } from '@headlessui/vue'
  import { CheckIcon, ChevronUpDownIcon } from '@heroicons/vue/20/solid'
  
  const languages = [
      { id: 1, name: 'ES', src: "../src/assets/img/es.png" },
      { id: 2, name: 'EN', src: "../src/assets/img/en.png" },
      { id: 3, name: 'FR', src: "../src/assets/img/fr.png" },
      { id: 4, name: 'IT', src: "../src/assets/img/it.png" },
      { id: 5, name: 'DE', src: "../src/assets/img/de.png" },
    ]
  
  const selected = ref(languages[0])
  </script>