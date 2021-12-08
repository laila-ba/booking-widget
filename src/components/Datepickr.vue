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
  name: "datepickr",
  props: ["modelValue"],
  emits: ["update:modelValue"],

  data() {
    return {
      date: null,
      config: {
        dateFormat: "D-F-j-Y",
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
