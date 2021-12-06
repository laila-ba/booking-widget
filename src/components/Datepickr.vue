<template>
  <label>Select date</label>
  <div class="mx-auto">
    <flatpickr
      :config="config"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    >
    </flatpickr>
  </div>
</template>

<script>
import flatpickr from "vue-flatpickr-component";

export default {
  name: "datepickr",
  props: ["modelValue"],
  emits: ["update:modelValue"],

  data() {
    return {
      date: null,
      dateFormat: "Y-m-d",
      config: {
        inline: true,
        minDate: "today",
      },
    };
  },
  components: {
    flatpickr,
  },
};
</script>
