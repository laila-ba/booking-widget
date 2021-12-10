<template>
  <a
    @click="selectTime(n)"
    class="p-4 rounded-full block mt-2 border rounded"
    :class="{ 'color text-white': timeSelected == n }"
    v-for="(n, key) in times"
    :key="key"
  >
    {{ n }}
  </a>
  <input type="hidden" @input="selectTime(timeSelected)" :value="modelValue" />
</template>

<script>
export default {
  emits: ["update:modelValue"],
  props: {
    start: {
      type: String,
      default: "12:00AM",
    },
    end: {
      type: String,
      default: "11:00PM",
    },

    interval: {
      type: Number,
      default: 30,
      validator: (val) => val > 0,
    },
    modelValue: {},
  },
  data() {
    return {
      timeSelected: null,
    };
  },

  methods: {
    selectTime(n) {
      this.timeSelected = n;
      this.$emit("update:modelValue", n);
    },
  },

  computed: {
    times() {
      var times = []; // time array
      var startTime = 0; // start time
      var ap = ["AM", "PM"]; // AM-PM

      //loop to increment the time and push results in array
      for (var i = 0; startTime < 24 * 60; i++) {
        var hh = Math.floor(startTime / 60); // get starting hours of day in 0-24 format
        var mm = startTime % 60; // get starting minutes of the hour in 0-55 format
        let hr = ("0" + (hh % 12)).slice(-2);
        times[i] =
          (hr === "00" ? "12" : hr) +
          ":" +
          ("0" + mm).slice(-2) +
          ap[Math.floor(hh / 12)]; // pushing data in array in [00:00 - 12:00 AM/PM format]
        startTime = startTime + this.interval;
      }

      return times.slice(
        times.findIndex((time) => time === this.start),
        times.findIndex((time) => time === this.end) + 1
      );
    },
  },
};
</script>
<style scoped>
.color {
  background: rgb(184, 49, 47);
}
</style>
