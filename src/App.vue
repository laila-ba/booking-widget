<template>
  <div class="flex w-full grid place-items-center">
    <div v-if="step < 4" class="my-5 px-5 w-1/4 overflow-hidden border-2">
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
      <p class="text-2xl pt-4">Select Your Service</p>

      <div v-if="form.service">
        <strong>{{
          services.find((service) => service.id === form.service).name
        }}</strong>
      </div>

      <p>Step {{ step }}</p>
      <div v-if="step === 3">
        <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
          <p class="text-gray-500 text-xs mb-2">DATE</p>
          <strong>{{ date }}</strong>
        </div>
        <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
          <p class="text-gray-500 text-xs mb-2">TIME</p>
          <strong>{{ fromTime }}-{{ toTime }}</strong>
        </div>
      </div>
      <div v-if="step > 1 && step < 4" class="mt-8">
        <button
          class="
            bg-yellow-600
            hover:bg-yellow-700
            text-white
            font-bold
            py-2
            px-4
            mb-4
            rounded-full
          "
          @click="next"
          v-if="step == 2"
        >
          Next
        </button>
        <button
          class="
            bg-yellow-600
            hover:bg-yellow-700
            text-white
            font-bold
            py-2
            px-4
            mb-4
            rounded-full
            ml-4
          "
          @click="prev"
          v-if="step > 1"
        >
          Back
        </button>
      </div>
    </div>

    <div class="w-3/4 justify-between">
      <div v-if="step === 1">
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

      <div
        class="box-border w-2/4 h-full p-4 border-4 mx-auto"
        v-if="step === 2"
      >
        <h1 class="text-2xl">Pick a Date and Time</h1>
        <div class="p-4 mt-5">
          <Datepickr v-model="date"> </Datepickr>
          <Timepickr v-model="time"> </Timepickr>
        </div>
      </div>

      <div v-if="step === 3">
        <div class="mx-auto w-2/4">
          <BookingForm @next="next" @form="captureFormData"> </BookingForm>
        </div>
      </div>

      <div v-if="step === 4">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-24 w-24 mx-auto"
          fill="none"
          viewBox="0 0 24 24"
          stroke="orange"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 13l4 4L19 7"
          />
        </svg>
        <h1 class="text-3xl mb-8">Booking Successful!</h1>
        <p>
          Thanks for your booking. One of our consultants will contact you soon.
        </p>
        <div v-if="form.service">
          <h3 class="mt-8">
            <strong>{{
              services.find((service) => service.id === form.service).name
            }}</strong>
          </h3>
        </div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-7 w-7 mx-auto mb-8"
          viewBox="0 0 20 20"
          fill="orange"
        >
          <path
            fill-rule="evenodd"
            d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z"
            clip-rule="evenodd"
          />
        </svg>
        <div class="flex-none inline-flex">
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-left p-4">
            <p class="text-gray-500 text-xs mb-2">DATE</p>
            <strong>{{ date }}</strong>
          </div>
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-left p-4">
            <p class="text-gray-500 text-xs mb-2">TIME</p>
            <strong>{{ time }}</strong>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Datepickr from "./components/Datepickr.vue";
import Timepickr from "./components/Timepickr.vue";
import BookingForm from "./components/Form.vue";
//import Vue from "vue";
import "flatpickr/dist/flatpickr.css";

export default {
  name: "App",
  data() {
    return {
      date: null,
      fromTime: null,
      toTime: this.fromTime++,
      form: {
        service: null,
      },
      formData: {},
      //bus: new Vue(),

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
    };
  },
  components: {
    Datepickr,
    Timepickr,
    BookingForm,
  },
  computed: {},
  methods: {
    captureFormData(e) {
      this.formData = e;
    },
    next() {
      this.step++;
      //if (this.step == 1) {
      //this.step++;
      // }
      // if (this.step == 2) {
      //   this.step++;
      // }
      // if (this.step == 3) {
      //   this.step++;
      // }
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
[type="text"],
[type="email"],
textarea,
select {
  padding: 10px;
  margin: 10px;
  /* a: left; */
  background-color: #fff;
  border-color: #d1d5db !important;
  border-width: 1px !important;
  border-radius: 5px !important;
}

.flatpickr-calendar {
  margin: 0 auto;
}
.flatpickr-calendar.inline {
  position: relative !important;
}
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
.date {
  min-width: 10rem;
}
</style>
