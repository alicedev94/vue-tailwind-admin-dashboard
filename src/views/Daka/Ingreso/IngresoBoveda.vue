<template>
  <AdminLayout>
    <PageBreadcrumb :pageTitle="currentPageTitle" />
    <div class="grid grid-cols-1 gap-6 sm:grid-cols-2">
      <div class="space-y-6">
        <ComponentCard title="Información del Cliente">
          <!-- Document Input -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              C.I / RIF
            </label>
            <div class="relative">
              <span
                class="absolute left-0 top-1/2 -translate-y-1/2 border-r border-gray-200 px-3.5 py-3 text-gray-500 dark:border-gray-800 dark:text-gray-400"
              >
                <SearchIcon />
              </span>
              <input
                v-model="document"
                type="text"
                placeholder="J-12345678-9"
                class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 pl-[62px] text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
              />
            </div>
          </div>

          <!-- Nombre del Cliente -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Nombre del Cliente
            </label>
            <input
              v-model="formData.CardName"
              type="text"
              placeholder="Nombre del Cliente"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
            />
          </div>

          <!-- Monto -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Monto
            </label>
            <input
              v-model.number="formData.amount"
              type="number"
              placeholder="0.00"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
            />
          </div>

          <!-- Detalles -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Detalles
            </label>
            <textarea
              v-model="formData.details"
              placeholder="Ingrese detalles de la operación"
              rows="3"
              class="dark:bg-dark-900 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
            ></textarea>
          </div>

          <div class="flex items-center gap-5">
            <Button @click="handleSubmit" size="sm" variant="primary" :endIcon="BoxIcon" :loading="loading" :disabled="loading">
              Procesar Ingreso
            </Button>
          </div>
        </ComponentCard>
      </div>
      <div class="space-y-6">
        <ComponentCard title="Información Adicional">
          <!-- Sucursal Origen -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Sucursal Origen
            </label>
            <select
              v-model="formData.sourceBPLName"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90"
            >
              <option value="Sucursal Punto Fijo">Sucursal Punto Fijo</option>
              <option value="Casa Central">Casa Central</option>
              <option value="Sucursal Maracaibo">Sucursal Maracaibo</option>
            </select>
          </div>

          <!-- Fecha del Documento -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Fecha del Documento
            </label>
            <input
              v-model="formData.documentDate"
              type="date"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90"
            />
          </div>

          <!-- Moneda -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Moneda
            </label>
            <select
              v-model="formData.CurrCode"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90"
            >
              <option value="USD">USD - Dólar Americano</option>
              <option value="VES">VES - Bolívar</option>
              <option value="EUR">EUR - Euro</option>
            </select>
          </div>

          <!-- Tasa de Cambio -->
          <div class="mb-4">
            <label class="mb-1.5 block text-sm font-medium text-gray-700 dark:text-gray-400">
              Tasa de Cambio
            </label>
            <input
              v-model.number="formData.rate"
              type="number"
              step="0.01"
              placeholder="0.00"
              class="dark:bg-dark-900 h-11 w-full rounded-lg border border-gray-300 bg-transparent px-4 py-2.5 text-sm text-gray-800 shadow-theme-xs placeholder:text-gray-400 focus:border-brand-300 focus:outline-hidden focus:ring-3 focus:ring-brand-500/10 dark:border-gray-700 dark:bg-gray-900 dark:text-white/90 dark:placeholder:text-white/30 dark:focus:border-brand-800"
            />
          </div>

          <!-- Error Message -->
          <div v-if="error" class="mt-4 p-3 bg-red-100 text-red-700 rounded-lg">
            {{ error }}
          </div>
        </ComponentCard>
      </div>
    </div>
  </AdminLayout>
</template>

<script setup>
import { reactive, ref, onMounted } from 'vue'
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
  userId: "1b10a7fe-1173-4a37-86b4-95eeede83310",
  CardCode: "",
  CardName: "",
  BPLName: "Casa Central",
  sourceBPLName: "Sucursal Punto Fijo",
  destinationBPLName: null,
  sourceBankName: null,
  destinationBankName: null,
  PrjName: null,
  accountDate: new Date().toISOString(),
  dueDate: new Date().toISOString(),
  documentDate: new Date().toISOString(),
  amount: 0,
  OPId: "048722d3-3648-4b20-a6f8-882b109c3c6a",
  CFWName: "Flujo de caja de actividades de operación",
  details: "",
  CurrCode: "USD",
  AcctCode: "1210010201091",
  monetaryAcctCode: "1101010201090",
  move: "client",
  rate: 67.63,
  BranchOcrCode: "CC00001",
  DepartmentOcrCode: null
})

const document = ref('')
const loading = ref(false)
const error = ref(null)

const handleSubmit = async () => {
  try {
    if (!document.value || !formData.amount || !formData.details) {
      error.value = "Por favor complete todos los campos obligatorios"
      return
    }

    loading.value = true
    error.value = null

    // Asignar el documento al CardCode
    formData.CardCode = document.value

    // Formatear fechas en ISO
    formData.accountDate = new Date(formData.accountDate).toISOString()
    formData.dueDate = new Date(formData.dueDate).toISOString()
    formData.documentDate = new Date(formData.documentDate).toISOString()

    console.log("Enviando datos:", formData)

    // Aquí harías la petición con axios
    // const response = await axios.post('api/ingresos-boveda', formData)
    // console.log('Respuesta:', response.data)

    // Simulamos una respuesta exitosa
    setTimeout(() => {
      loading.value = false
      alert('Datos enviados con éxito')
      document.value = ''
      formData.CardName = ''
      formData.amount = 0
      formData.details = ''
    }, 1000)

  } catch (err) {
    console.error("Error al enviar datos:", err)
    error.value = "Ha ocurrido un error al procesar la solicitud"
    loading.value = false
  }
}

// Formatear las fechas iniciales para el input type="date"
onMounted(() => {
  const formatDate = (dateString) => {
    const date = new Date(dateString)
    return date.toISOString().split('T')[0]
  }

  formData.documentDate = formatDate(new Date())
  formData.accountDate = formatDate(new Date())
  formData.dueDate = formatDate(new Date())
})
</script>
