<template>
  <div
    class="
      flex
      grid-row
      stretched-mobile stretched-tablet
      py-0
      pl-0
      w-full
      col20
    "
  >
    <div
      v-if="step < 4"
      class="
        booking-widget
        p-7
        w-1/4
        overflow-hidden
        f-left
        flex-col
        text-center
        items-center
        justify-center
      "
    >
      <div v-if="step === 1">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-12 w-12 m-auto mt-16"
          viewBox="0 0 20 20"
          fill="#b8312F"
        >
          <path
            d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z"
          />
        </svg>
        <p class="text-2xl pt-4">Select Your Service</p>
      </div>
      <div class="mt-4 text-sm text-gray-500">
        <div v-if="form.service" class="text-2xl mt-16">
          {{ services.find((service) => service.id === form.service).name }}
        </div>
        <p class="mt-4">Health & Nutrition Cooking Show</p>
      </div>

      <p class="mt-8">Step {{ step }}</p>
      <div v-if="step === 2">
        <div v-if="newDate">
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
            <p class="text-gray-500 text-xs mb-2">DATE</p>
            {{ newDate }}
          </div>
        </div>
        <div v-else>
          {{ todaysdate }}
        </div>
        <div v-if="form.fromTime">
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
            <p class="text-gray-500 text-xs mb-2">TIME</p>
            {{ form.fromTime }} to {{ toTime }}
          </div>
        </div>
        <div v-else>
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
            <p class="text-gray-500 text-xs mb-2">TIME</p>
          </div>
        </div>
      </div>
      <div v-if="step === 3">
        <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
          <p class="text-gray-500 text-xs mb-2">DATE</p>
          {{ newDate }}
        </div>
        <div class="date bg-gray-300 bg-opacity-25 m-4 text-center p-4">
          <p class="text-gray-500 text-xs mb-2">TIME</p>
          {{ form.fromTime }} to {{ toTime }}
        </div>
      </div>
      <div v-if="step > 1 && step < 4" class="mt-8">
        <button
          class="text-white font-bold py-2 px-4 mb-4 rounded-full"
          style="background-color: #b8312f"
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
            inline-flex
          "
          style="background-color: #b8312f"
          @click="prev"
          v-if="step > 1"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M7 16l-4-4m0 0l4-4m-4 4h18"
            />
          </svg>

          Back
        </button>
      </div>
    </div>

    <div class="w-3/4 justify-between bg-gray-50">
      <div v-if="step === 1" class="flex w-full grid place-items-center p-7">
        <div class="w-full text-2xl text-left">
          <h2>Select Your Service</h2>
          <hr class="w-52 mt-4" />
        </div>
        <div
          class="
            justify-between
            container-widget
            m-auto
            flex flex-wrap
            overflow-hidden
            p-10
          "
        >
          <div
            class="
              my-5
              p-8
              w-2/5
              overflow-hidden
              border border-opacity-100
              cursor-pointer
              bg-white
              rounded-md
            "
            v-for="service in services"
            :key="service.id"
          >
            <div class="relative w-24 h-24 mx-auto mb-4 b-center bg-cover">
              <div v-html="service.icon" @click="changeService(service)"></div>
            </div>

            <p class="text-base pt-4 text-gray-500">{{ service.name }}</p>
            <p class="text-sm text-gray-500">{{ service.duration }}</p>
          </div>
        </div>
      </div>

      <div class="" v-if="step === 2">
        <div class="w-full text-2xl text-left mt-8 ml-8">
          <h2>Pick a Date and Time</h2>
          <hr class="w-52 mt-4" />
        </div>
        <div class="p-4 mt-5 inline-flex cursor-pointer">
          <Datepickr v-model="form.date" class="invisible"> </Datepickr>
          <div class="ml-12 p-8 overflow-y-auto" style="max-height: 450px">
            <TimeSlot
              v-model="form.fromTime"
              :interval="30"
              start="09:00AM"
              end="04:00PM"
            />
          </div>
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
          stroke="#b8312f"
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
          fill="#b8312f"
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
            {{ newDate }}
          </div>
          <div class="date bg-gray-300 bg-opacity-25 m-4 text-left p-4">
            <p class="text-gray-500 text-xs mb-2">TIME</p>
            {{ form.fromTime }} to {{ toTime }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Datepickr from "./components/Datepickr.vue";
import TimeSlot from "./components/TimeSlot.vue";
import BookingForm from "./components/Form.vue";
import "flatpickr/dist/flatpickr.css";

export default {
  name: "App",
  data() {
    return {
      todaysdate: new Intl.DateTimeFormat("default", {
        dateStyle: "long",
      }).format(new Date()),
      form: {
        service: null,
        date: null,
        fromTime: null,
        formData: {},
      },
      step: 1,
      services: [
        {
          id: "Home",
          name: "In Home Cooking Presentation",
          duration: "60mins",
          icon: `<img class="rounded-full border border-gray-100 shadow-sm w-24 h-24" src="https://content.app-sources.com/s/74861868789532732/thumbnails/160x120/Images/home-cooked-happiness-2021-08-28-15-39-31-utc_1-6379364.jpg" alt="user image" />`,
        },
        {
          id: "Virtual",
          name: "Virtual Video Presentation",
          duration: "60mins",
          icon: ` <img class="rounded-full border border-gray-100 shadow-sm w-24 h-24" src="https://content.app-sources.com/s/74861868789532732/thumbnails/160x120/Images/cooking-at-home-2021-08-27-17-18-37-utc_1-6379367.jpg" alt="user image" />`,
        },
      ],
    };
  },
  components: {
    Datepickr,
    TimeSlot,
    BookingForm,
  },
  computed: {
    toTime: {
      get: function () {
        var x = this.form.fromTime;
        var y = x ? x.split(/:/) : [];
        y[0]++;
        y = `${y[0] + ":" + y[1]}`;
        return y;
      },
    },
    newDate: {
      get: function () {
        const date = new Date(this.form.date);
        return new Intl.DateTimeFormat("default", { dateStyle: "long" }).format(
          date
        );
      },
    },
  },
  methods: {
    captureFormData(e) {
      this.form.formData = e;
    },
    next() {
      if (this.step == 2) {
        if (this.form.fromTime && this.form.date) {
          return this.step++;
        }
      }
      if (this.step == 1 || this.step == 3) {
        this.step++;
      }
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
.booking-widget {
  box-shadow: 0px 0px 25px 0px rgb(170 170 170 / 25%);
  height: inherit;
}
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
  width: 23rem;
}
.flatpickr-day.today {
  border-color: #fff;
}
.flatpickr-day.today:hover {
  border-color: #b8312f;
  background: #b8312f;
  color: #fff;
}
.flatpickr-day:hover {
  border-color: #b8312f;
  background: #b8312f;
  color: #fff;
}
.flatpickr-calendar {
  margin: 0 auto;
  -webkit-box-shadow: none !important;
}
.flatpickr-calendar.inline {
  position: relative !important;
  width: 500px;
  height: 300px;
  background-color: rgba(249, 250, 251, var(--tw-bg-opacity));
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 70%;
  margin: 0 auto;
}
.container-widget {
  width: 100%;
  margin: 0 auto;
}
.flatpickr-current-month {
  margin-bottom: 3rem;
  font-size: 1.4rem;
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
hr {
  color: #b8312f !important;
}

.flatpickr-innerContainer {
  margin-left: 100px;
  margin-top: 1rem;
}
.daycontainer {
  height: 300px !important;
}
span.flatpickr-weekday {
  padding: 12px 7px;
  font-size: 1rem;
}
.flatpickr-day.selected {
  background: rgb(184, 49, 47);
  border-color: rgb(184, 49, 47);
}
.flatpickr-day.selected:hover {
  background: rgb(184, 49, 47);
  border-color: rgb(184, 49, 47);
}
.flatpickr-day {
  font-size: 1rem;
  background: rgba(0, 0, 0, 0.04);
}
</style>
