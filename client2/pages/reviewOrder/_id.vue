<template>
  <div class="container">
    <h2 class="review text-center">รีวิว</h2>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="เขียนรีวิว:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-textarea
          id="input-1"
          v-model="form.review"
          placeholder="กรุณราเขียนรีวิวติวเตอร์ดังกล่าว..."
          rows="3"
          required
        ></b-form-textarea>
        <!-- <b-form-input id="input-1" v-model="form.email" required placeholder="Enter email"></b-form-input> -->
      </b-form-group>

      <b-form-group id="input-group-3" label="Rating:" label-for="input-3">
        <b-form-rating id="input-3" v-model="form.rating" variant="warning" class="mb-2" required></b-form-rating>
        <p class="mt-2">Value: {{ form.rating }}</p>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
import Strapi from "strapi-sdk-javascript/build/main";
import axios from "axios";
const apiUrl = process.env.API_URL || "http://localhost:1337";
const strapi = new Strapi(apiUrl);
export default {
  data() {
    return {
      form: {
        review: "",
        rating: null,
      },
      show: true,
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      console.log(JSON.stringify(this.form));
      axios.put(apiUrl + "/orders/" + this.$route.params.id, {
        review:this.form.review,
        rating:this.form.rating
      }).then(res => {
        console.log(res)
      })
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.review = "";

      this.form.rating = null;
    },
  },
};
</script>

<style>
h2 {
  padding-top: 2rem;
}
</style>