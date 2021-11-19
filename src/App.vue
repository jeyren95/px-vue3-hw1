<template>
  <main class="bg-gray-50">
    <div class="max-w-6xl mx-auto px-3 py-12 space-y-6">
      <div class="mb-8">
        <div>
          <h1 class="text-6xl mb-4 font-extrabold">Careers</h1>
        </div>
      </div>
      <div class="flex flex-col md:flex-row gap-3">
        <div class="md:w-1/2">
          <form @submit.prevent="handleSubmit">
            <div class="bg-white overflow-hidden shadow rounded-lg divide-y divide-gray-200">
              <div class="px-4 py-5 sm:px-6 text-lg">Add Job Posting</div>
              <div class="px-4 py-5 sm:p-6">
                <div class="space-y-5">
                  <div class="lg:grid lg:grid-cols-3 lg:gap-4 lg:items-start">
                    <Label id="job-title" label="Job Title" />
                    <div class="mt-1 sm:mt-0 sm:col-span-2">
                      <!-- when used on a component, v-model translates to the following -->
                      <!-- in Vue3 =====> :model-value="title", @update:model-value="title = input value" -->
                      <!-- in Vue2 =====> :value="title", @input="title = input value" -->
                      <Input 
                      type="text" 
                      id="job-title" 
                      required="true" 
                      name="job-title" 
                      v-model="title" 
                      />
                    </div>
                  </div>

                  <div class="lg:grid lg:grid-cols-3 lg:gap-4 lg:items-start">
                    <Label id="job-level" label="Job Level" />
                    <div class="mt-1 sm:mt-0 sm:col-span-2">
                      <Select 
                      id="job-level" 
                      required="true"
                      name="job-level" 
                      :selectOptions="selectOptions"
                      v-model="level"
                       />
                    </div>
                  </div>

                  <div class="lg:grid lg:grid-cols-3 lg:gap-4 lg:items-start">
                    <Label id="job-department" label="Department" />
                    <div class="mt-1 sm:mt-0 sm:col-span-2">
                      <Input 
                      type="text" 
                      id="job-department" 
                      required="true" 
                      name="job-department" 
                      placeholder="e.g. Engineering"
                      v-model="department"
                      />
                    </div>
                  </div>

                  <div class="lg:grid lg:grid-cols-3 lg:gap-4 lg:items-start">
                    <Label id="job-summary" label="Summary" />
                    <div class="mt-1 sm:mt-0 sm:col-span-2">
                      <TextArea 
                      id="job-summary" 
                      required="true" 
                      name="job-summary" 
                      rows="4" 
                      v-model="summary"
                      />
                    </div>
                  </div>

                  <div class="mt-1 sm:mt-0 sm:col-span-2">
                    <div class="relative w-32">
                      <Button 
                      type="button"
                      class="absolute left-0 inset-y-0 px-1.5 text-gray-400"
                      @click="decreaseHeadcount"
                      >
                        <MinusIcon class="h-5 w-5" />
                      </Button>
                      <Input 
                      type="text" 
                      name="headcount" 
                      id="headcount" 
                      required="true" 
                      class="px-9 text-center"
                      v-model="headcount"
                      readonly="true"
                      />
                      <Button 
                      type="button"
                      class="absolute right-0 inset-y-0 px-1.5 text-gray-400"
                      @click="increaseHeadcount"
                      >
                        <PlusIcon class="h-5 w-5" />
                      </Button>
                    </div>
                  </div>

                </div>
              </div>

              <div class="px-4 py-4 sm:px-6 text-right">
                <Button 
                type="submit"
                class="
                inline-flex 
                justify-center 
                py-2 
                px-4 
                border border-transparent
                shadow-sm
                text-sm
                font-medium
                rounded-md
                text-white
                bg-pink-600 
                hover:bg-pink-700 
                focus:outline-none 
                focus:ring-2 
                focus:ring-offset-2 
                focus:ring-pink-500" 
                name="ADD"
                />
              </div>
            </div>
          </form>
        </div>

        <ul v-if="jobPostings.length > 0" class="md:flex-1 space-y-3">
          <CareerItem 
          v-for="(jobPosting, index) in jobPostings"
          :key="index"
          :job="jobPosting"
          @remove-job-posting="removeJobPosting"
          />      
        </ul>
        <h1 v-else>No job postings yet!</h1>
      </div>
    </div>
  </main>
</template>

<script>
import Label from "./components/Label.vue"
import Input from "./components/Input.vue"
import Select from "./components/Select.vue"
import Button from "./components/Button.vue"
import TextArea from "./components/TextArea.vue"
import CareerItem from "./components/CareerItem.vue"

import { MinusIcon, PlusIcon } from "@heroicons/vue/solid"

export default {
  name: 'App',
  components: {
    Label,
    Input,
    Select,
    Button,
    TextArea,
    MinusIcon,
    PlusIcon,
    CareerItem
  },
  data() {
    return {
      jobPostings: [],    
      title: "",
      department: "",
      level: "Internship",
      summary: "",
      headcount: 1,
      selectOptions: ["Internship", "Entry", "Experienced", "Manager"]
    }
  },
  methods: {
    handleSubmit() {
      let newJobPosting = {
        title: this.title,
        department: this.department,
        level: this.level,
        summary: this.summary,
        headcount: this.headcount
      }
      console.log(newJobPosting)
      this.jobPostings.push(newJobPosting)

      this.title = ""
      this.department = ""
      this.level = "Internship"
      this.summary = ""
      this.headcount = 1
    },
    increaseHeadcount() {
      this.headcount++
    },
    decreaseHeadcount() {
      this.headcount > 1 && this.headcount--
    },
    removeJobPosting(jobToRemove) {
      this.jobPostings = this.jobPostings.filter((jobPosting) => jobPosting !== jobToRemove)
    }
  }

}
</script>

