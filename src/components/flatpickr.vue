<template>
  <label>Select date</label>
  <div class="object-center">
    <flatpickr :config="config"> </flatpickr>
  </div>
</template>

<script>
import flatpickr from "vue-flatpickr-component";

export default {
  name: "DatePickr",
  data() {
    return {
      date: null,
      dateFormat: "Y-m-d",
      config: {
        inline: true,
      },
    };
  },
  components: {
    flatpickr,
  },
};
</script>
