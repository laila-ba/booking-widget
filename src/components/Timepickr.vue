<template>
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
  name: "Timepickr",
  props: ["modelValue"],
  emits: ["update:modelValue"],

  data() {
    return {
      date: null,
      dateFormat: "H:i",
      config: {
        noCalendar: true,
        inline: true,
        enableTime: true,
      },
    };
  },
  components: {
    flatpickr,
  },
};
</script>
