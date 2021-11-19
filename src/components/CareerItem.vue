<template>
  <li class="js-career-item">
    <div class="bg-white shadow overflow-hidden sm:rounded-md">
      <div class="px-4 py-4 flex items-center sm:px-6">
        <div class="min-w-0 flex-1 sm:flex sm:items-center sm:justify-between">
          <div>
            <div class="text-sm leading-5 font-medium text-pink-600 truncate">
              {{ job.title }}
              <span class="ml-1 font-normal text-gray-500">
                in {{ job.department }}
              </span>
            </div>
            <div class="mt-2 flex">
              <div class="flex items-center gap-2 text-sm leading-5 text-gray-500">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="flex-shrink-0 mr-1.5 h-5 w-5 text-gray-400">
                  <path fill-rule="evenodd" d="M6 6V5a3 3 0 013-3h2a3 3 0 013 3v1h2a2 2 0 012 2v3.57A22.952 22.952 0 0110 13a22.95 22.95 0 01-8-1.43V8a2 2 0 012-2h2zm2-1a1 1 0 011-1h2a1 1 0 011 1v1H8V5zm1 5a1 1 0 011-1h.01a1 1 0 110 2H10a1 1 0 01-1-1z" clip-rule="evenodd"></path>
                  <path d="M2 13.692V16a2 2 0 002 2h12a2 2 0 002-2v-2.308A24.974 24.974 0 0110 15c-2.796 0-5.487-.46-8-1.308z"></path>
                </svg>
                <span>Level: {{ job.level }} </span>
                <Badge 
                v-if="job.level === 'Internship'"
                badgeText="Student-friendly"
                class="bg-green-100 text-green-800"
                />
              </div>
            </div>

          </div>
        </div>

        <div class="ml-5 flex-shrink-0 inline-flex items-center justify-center gap-2">
          <Button
          type="button"
          class="
          js-delete-btn
          p-1
          rounded-full
          hover:bg-gray-50
          focus:outline-none  
          focus:bg-gray-500 
          focus:ring
          focus:ring-pink-500
          focus:ring-opacity-30
          transition
          duration-150
          ease-in-out
          "
          @click="handleClick"
          >
            <TrashIcon class="h-5 w-5 text-gray-400" />
          </Button>
          
        </div>
      </div>
    </div>
  </li>
</template>

<script>
import Button from "./Button.vue"
import Badge from "./Badge.vue"

import { TrashIcon } from "@heroicons/vue/solid"

export default {
  components: {
    Button,
    Badge,
    TrashIcon
  },
  props: ["job"],
  methods: {
    handleClick() {
      this.$emit("remove-job-posting", this.job)
    }
  }
}

</script>