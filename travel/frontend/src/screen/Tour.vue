<script setup>
import { ref } from 'vue'
import {
  Dialog,
  DialogPanel,
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  Popover,
  PopoverButton,
  PopoverGroup,
  PopoverPanel,
} from '@headlessui/vue'
import {
  ArrowPathIcon,
  Bars3Icon,
  ChartPieIcon,
  CursorArrowRaysIcon,
  FingerPrintIcon,
  SquaresPlusIcon,
  XMarkIcon,
  ArrowLeftCircleIcon
} from '@heroicons/vue/24/outline'
import { ChevronDownIcon, PhoneIcon, PlayCircleIcon, UserCircleIcon, CheckIcon } from '@heroicons/vue/20/solid'


const mobileMenuOpen = ref(false)
</script>

<template>
  <div>
    <div class="m-6">
      <div class="w-12 mb-4">
        <router-link :to="{
          path: '/home',
        }">
          <ArrowLeftCircleIcon />
        </router-link>
      </div>
      <div class="group relative">
        <div
          class="aspect-h-1 aspect-w-1 w-full overflow-hidden rounded-md bg-gray-200 lg:aspect-none group-hover:opacity-75 lg:h-80">
          <!-- ถ้ามีให้ทำข้างหลังต่อไป ถ้าไม่มีทั้งก้อนเป็นundefined -->
          <img :src="place?.img" class="h-full w-full object-cover object-center lg:h-full lg:w-full rounded-2xl" />
        </div>
        <div class="bg-lightgreen rounded-2xl p-4 my-4 grid grid-cols-1 gap-x-6 gap-y-4 ">
          <h2 class=" text-2xl font-bold tracking-tight text-gray-900">{{ place?.name }}</h2>
          <div class="mt-1 flex justify-between">
            <div>
              <h3 class="text-sm text-gray-700">
                  {{ place?.province }}
              </h3>
              <p class="mt-1 text-sm text-gray-500">{{ place?.type }}</p>
            </div>
            <p class="text-sm font-medium text-gray-900">฿{{ place?.price }}</p>
          </div>
          <div>
            {{ place?.description }}
          </div>
          <router-link :to="{
          path: '/home',
          }">
            <div
              class="mt-10 block w-full rounded-md bg-darkgreen px-3 py-2 text-center text-sm font-semibold text-white shadow-sm
               hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
               >
              Back to Home
            </div>
          </router-link>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      place: null,
      nameSelected: '',
    };
  },

  created() {
    this.fetchPlaces();
  },
  methods: {
    async fetchPlaces() {
      console.log("fetchplaces")
      try {
        this.nameSelected = this.$route.params.name
        console.log(this.nameSelected)
        const response = await axios.get(`http://localhost:4000/places/${this.nameSelected}`);
        this.place = response.data; // Store the retrieved comments data in the 'comments' array
        console.log(this.place)
      } catch (error) {
        console.error('Error fetching place:', error);
      }
    },

  }
};

</script>
<style global lang="postcss">
body {
  @apply h-full bg-verylightgreen
}
</style>
