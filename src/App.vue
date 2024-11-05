<script setup>
import DatePicker from './components/DatePicker.vue'
import { DateTime } from 'luxon';
import { ref } from 'vue'

const dateRangeWithHours = ref({
  start: null,
  end: null
})

const dateRangeWithoutHours = ref({
  start: null,
  end: null
})

const changeRangeDate = dateRange => {
  dateRangeWithHours.value = dateRange
  console.log('el dateRange es', dateRange )
}

const changeRangeDateWithoutRange = dateRange => {
  dateRangeWithoutHours.value = dateRange
  console.log('el dateRange es', dateRange )
}

</script>

<template>
  <div>
    <h1>Date picker con vue3datepicker</h1>
    <section>
      <label> Con hora y sin fecha por defecto </label>
      <DatePicker 
        :range="true"
        @change-range-date="changeRangeDate"
        :date-picker-with-hours="true"
        :date-range="dateRangeWithHours"/>
      <span>
        Selección con hora ->
         Inicio: {{ !dateRangeWithHours.start ? '' : DateTime.fromJSDate(dateRangeWithHours.start).toFormat('dd/MM/yyyy HH:ss:mm') }}
         Fin: {{ !dateRangeWithHours.end ? '' : DateTime.fromJSDate(dateRangeWithHours.end).toFormat('dd/MM/yyyy HH:ss:mm') }}
      </span>
    </section>

    <section>
      <label> Con hora y sin fecha por defecto </label>
      <DatePicker 
        :range="true"
        @change-range-date="changeRangeDateWithoutRange"
        :date-range="dateRangeWithoutHours"/>
      <span>
        Selección con hora ->
         Inicio: {{ !dateRangeWithoutHours.start ? '' : DateTime.fromJSDate(dateRangeWithoutHours.start).toFormat('dd/MM/yyyy') }}
         Fin: {{ !dateRangeWithoutHours.end ? '' : DateTime.fromJSDate(dateRangeWithoutHours.end).toFormat('dd/MM/yyyy') }}
      </span>
    </section>
  </div>
</template>

