<template>
<form enctype="multipart/form-data" @submit.prevent="checkForm"  method="post">
<p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="(error,key) in errors" :key="key">{{ error }}</li>
    </ul>
  </p>
  <div class="form my-8  p-8 mx-auto">
    <div class="w-full text-2xl text-left mt-8 ml-8">
          <h2>Enter Your Details</h2>
          <hr class="w-52 mt-4 mb-8" />
        </div>
    <div>
      <label for="name" class="block text-xs text-gray-900 font-medium"
        >Name</label
      >
      <input
      v-model="form.name"
        name="name"
        required="true"
        type="text"
        label="Name"
        helper="Full Name"
      />
    </div>
    <div>
      <label for="email" class="block text-xs text-gray-900 font-medium"
        >Email</label
      >
      <input
      v-model="form.email"
        name="email"
        required="true"
        type="email"
        label="Email"
        helper="Email"
      />
    </div>
    <div>
      <label for="phone" class="block text-xs text-gray-900 font-medium"
        >Phone Number:</label
      >
      <input
      v-model="form.phone"
        name="phone"
        required="true"
        type="text"
        label="phone"
        helper="Phone"
      />
    </div>
    <div>
      <label for="Address" class="block text-xs text-gray-900 font-medium"
        >Address:</label
      >
      <input
      v-model="form.address"
        name="Address"
        required="true"
        type="text"
        label="Address"
        helper="Address"
      />
    </div>
    <div>
      <label for="Town" class="block text-xs text-gray-900 font-medium"
        >Town:</label
      >
      <input
      v-model="form.town"
        name="Town"
        required="true"
        type="text"
        label="Town"
        helper="Town"
      />
    </div>
    <div>
      <label for="County" class="block text-xs text-gray-900 font-medium"
        >County:</label
      >
      <input
      v-model="form.county"
        name="County"
        required="true"
        type="text"
        label="County"
        helper="County"
      />
    </div>
    <div>
      <label for="PostCode" class="block text-xs text-gray-900 font-medium"
        >Post Code:</label
      >
      <input
      v-model="form.postCode"
        name="PostCode"
        required="true"
        type="text"
        label="PostCode"
        helper="PostCode"
      />
    </div>
    <div>
      <label
        for="Country"
        required="true"
        class="block text-xs text-gray-900 font-medium"
        >Country:</label
      >
      <country-select
      v-model="form.country"
        class="p-4 m-4"
        :country="form.country"
        topCountry="US"
      />
    </div>
    <div>
      <button
        type="submit"
        class="
          color
          text-white
          py-2
          px-4
          ml-4
          w-full
          mt-4
        "
        @click="submitBooking()"
      >
        Book Appointment
      </button>
    </div>
  </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: null,
        email: null,
        phone: null,
        address: null,
        town: null,
        county: null,
        postCode: null,
        country: null,
      },
      errors: [],
      country: "",
      region: "",
    };
  },
  components: {},

  methods: {
    submitBooking() {
      console.log("submitted")
      this.$emit("form", this.form)
       this.$emit("next", true)
    },
    checkForm: function (e) {
       this.errors = [];

      if (!this.form.name) {
        this.errors.push("Name required.");
      }
      if (!this.form.email) {
        this.errors.push("email required.");
      }
    if (!this.errors.length > 0) {
        return true;
      }
      e.preventDefault();
    },
  },
};
</script>

<style scoped>
.form {
  text-align: left;
}
.color{
  background: rgb(184, 49, 47);
}
</style>
-->
