<template>
  <label>Select date</label>
  <flat-pickr> </flat-pickr>
</template>

<script>
import flatpickr from "flatpickr";

export default {
  name: "DatePickr",
  data() {
    return {
      date: null,
      dateFormat: "Y-m-d",
    };
  },
  components: {
    flatpickr,
  },
};
</script>
