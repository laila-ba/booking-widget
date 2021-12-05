<template>
  <div class="flex w-full">
    <div class="my-5 px-5 w-1/4 overflow-hidden">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-12 w-12 m-auto"
        viewBox="0 0 20 20"
        fill="orange"
      >
        <path
          d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z"
        />
      </svg>
      <p class="text-xl pt-4">Select Your Service</p>
      <!--
      <div>
        {{ services.find((service) => service.id === form.service).name }}
      </div>
      -->
      <p>Step {{ step }}</p>
    </div>

    <div class="w-3/4 justify-between">
      <div v-if="step === 1">
        <h1 class="text-2xl pb-10">Select your Service</h1>
        <div
          class="
            justify-between
            container-widget
            m-auto
            flex flex-wrap
            overflow-hidden
          "
        >
          <div
            class="
              my-5
              px-5
              w-2/5
              overflow-hidden
              border border-opacity-100
              cursor-pointer
            "
            v-for="service in services"
            :key="service.id"
          >
            <div v-html="service.icon" @click="changeService(service)"></div>

            <p class="text-xl pt-4">{{ service.name }}</p>
            <p>{{ service.duration }}</p>
          </div>
        </div>
      </div>

      <div v-if="step === 2">
        <h1>Pick a Date and Time</h1>
        <flatpickr> </flatpickr>
      </div>

      <div v-if="step === 3">step3</div>

      <div v-if="step === 4">step4</div>

      <div>
        <button
          class="
            bg-blue-500
            hover:bg-orange-700
            text-white
            font-bold
            py-2
            px-4
            rounded
          "
          @click="next"
          v-if="step < 4"
        >
          Next
        </button>
        <button
          class="
            bg-transparent
            hover:bg-orange-500
            text-blue-700
            font-semibold
            hover:text-white
            py-2
            px-4
            border border-blue-500
            hover:border-transparent
            rounded
          "
          @click="prev"
          v-if="step > 1"
        >
          Back
        </button>
        <pre>
          {{ form }}
        </pre>
      </div>
    </div>
  </div>
</template>

<script>
import flatpickr from "./components/flatpickr.vue";

export default {
  name: "App",
  data() {
    return {
      form: {
        service: null,
      },
      step: 1,
      services: [
        {
          id: "Home",
          name: "In Home Cooking Presentation",
          duration: "60mins",
          icon: `<svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 m-auto" viewBox="0 0 20 20" fill="orange">
            <path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z" />
          </svg>`,
        },
        {
          id: "Virtual",
          name: "Virtual Video Presentation",
          duration: "60mins",
          icon: ` <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 m-auto" viewBox="0 0 20 20" fill="orange">
          <path d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z" />
        </svg>`,
        },
      ],

      showDate: false,
    };
  },
  components: {
    flatpickr,
  },
  computed: {},
  methods: {
    next() {
      this.step++;
    },
    prev() {
      this.step--;
    },
    changeService(service) {
      this.form.service = service.id;
      this.next();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container-widget {
  width: 92%;
  margin: 0 auto;
}
.m-auto {
  margin: 0 auto;
}
.bookingName svg {
  margin: 0 auto;
}
.bookingName {
  margin-right: 0;
  margin-bottom: 20px;
  margin-top: 100px;
  max-width: 300px;
  height: 300px;
  margin-left: 5rem;
}
</style>
