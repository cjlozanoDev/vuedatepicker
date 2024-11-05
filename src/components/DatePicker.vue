<script setup>
import { computed } from 'vue';
import { es } from 'date-fns/locale';
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

const emit = defineEmits(['change-range-date', 'change-range-date-without-range'])

const props = defineProps({
  range: {
    type: Boolean,
    default: false
  },
  dateRange: {
    type: Object,
    default: () => ({})
  },
  datePickerWithHours: {
    type: Boolean,
    default: false
  } 
})


const dateRangeSelected = computed({
  get() {
    if (!props.dateRange || (!props.dateRange.start && !props.dateRange.end)) return null;
    return [props.dateRange.start, props.dateRange.end]
  },
  set(newValue) {
    const objectDate = {
      start: newValue ? newValue[0] : null,
      end: newValue ? newValue[1] : null
    }
    emit('change-range-date', objectDate)
  }
})


</script>

<template>
  <div>
    <VueDatePicker 
      v-if="datePickerWithHours"
      v-model="dateRangeSelected"
      locale="es" 
      :format-locale="es"
      format="dd/MM/yyyy HH:mm:ss"
      :range="range"
      cancel-text="Cerrar"
      select-text="Seleccionar"/>
    <VueDatePicker
      v-else
      :enable-time-picker="false"
      v-model="dateRangeSelected"
      locale="es" 
      :format-locale="es"
      format="dd/MM/yyyy"
      :range="range"
      cancel-text="Cerrar"
      select-text="Seleccionar" />
  </div>
</template>