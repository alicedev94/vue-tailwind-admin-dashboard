<template>
  <AdminLayout>
    <PageBreadcrumb :pageTitle="currentPageTitle" />
    <div class="grid grid-cols-1 gap-6 sm:grid-cols-2">
      <div class="space-y-6">
        <ComponentCard title="Carga">
          <!-- Email Input -->
          <div>
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Email
            </label>
            <div class="relative">
              <span
                class="absolute left-0 top-1/2 -translate-y-1/2 border-r border-gray-200 px-3.5 py-3 text-gray-500 dark:border-gray-800 dark:text-gray-400"
              >
                <SearchIcon />
              </span>
              <input
                v-model="email"
                type="text"
                placeholder="info@gmail.com"
                class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 pl-[62px] text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
              />
            </div>
          </div>

          <div class="flex items-center gap-5">
            <Button @click="handleSubmit" size="sm" variant="primary" :endIcon="BoxIcon">
              Aceptar
            </Button>
          </div>
        </ComponentCard>
      </div>
      <div class="space-y-6">
        <ComponentCard title="Checkboxes">
          <CheckboxInput />
        </ComponentCard>

        <ComponentCard title="Inputs Group"> <InputGroup /> </ComponentCard>
      </div>
    </div>
  </AdminLayout>
</template>

<script setup>
import { reactive, ref } from 'vue'
import PageBreadcrumb from '@/components/common/PageBreadcrumb.vue'
import AdminLayout from '@/components/layout/AdminLayout.vue'
import DefaultInputs from '@/components/forms/FormElements/DefaultInputs.vue'
import ComponentCard from '@/components/common/ComponentCard.vue'
import SelectInput from '@/components/forms/FormElements/SelectInput.vue'
import InputState from '@/components/forms/FormElements/InputState.vue'
import TextArea from '@/components/forms/FormElements/TextArea.vue'
import InputGroup from '@/components/forms/FormElements/InputGroup.vue'
import Dropzone from '@/components/forms/FormElements/Dropzone.vue'
import FileInput from '@/components/forms/FormElements/FileInput.vue'
import CheckboxInput from '@/components/forms/FormElements/CheckboxInput.vue'

import SearchIcon from '@/icons/SearchIcon.vue'


import Button from '@/components/ui/Button.vue'
import { BoxIcon } from '@/icons'

const currentPageTitle = ref('Ingreso Boveda')

const formData = reactive({
  input: '',
})

const handleSubmit = () => {
  console.log(formData)
}
</script>
