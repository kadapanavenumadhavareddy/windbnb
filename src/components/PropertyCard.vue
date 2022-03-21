<template>
  <div class="card">
    <img :src="data.photo" alt="image" />
    <section>
      <div class="body">
        <p class="body-host" v-if="data.superHost">Super Host</p>
        <p class="body-content">
          {{ data.type }}.<span v-if="beds(data.beds)"
            >{{ data.beds }} beds</span
          >
        </p>
      </div>
      <p class="body-rating">
        <span class="star">&#9733;</span>{{ data.rating }}
      </p>
    </section>
    <p class="card-title">{{ data.title }}</p>
  </div>
</template>
<script>
export default {
  props: ["data"],
  methods: {
    beds(val) {
      if (val == null) return false;
      else return true;
    },
  },
};
</script>
