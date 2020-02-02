<template>
  <nuxt-link :to="'detail/' + id">
    <div class="listsearch">
        <hr />
        <div class="row pointer">
          <div class="col-md-3">
            <img
              class="card-img-left img-fluid"
              :src="listsearch.imageUrl"
              alt
            />
          </div>

          <div class="col">
            <h4 class="title">{{listsearch.name}}</h4>

            <p>{{listsearch.description}}</p>
          </div>

          <div class="col-auto">
            <h4>ประกาศของ</h4>
            <p class="card-text">{{ listsearch.tutorName ||'No description provided' }}</p>
          </div>
        </div>
    </div>
  </nuxt-link>
</template>

<script>
export default {
  name: "Listsearch",
  props: ["listsearch", "id"]
};
</script>

<style scoped>

</style>
