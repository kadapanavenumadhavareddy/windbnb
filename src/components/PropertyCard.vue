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
<style scoped>
@media screen and (min-width: 400px) {
  img {
    height: 269px;
    width: 395px;
    border-radius: 24px;
  }
  p {
    font-size: 14px;
    line-height: 17px;
    color: #828282;
  }
  .star {
    font-size: 16px;
    color: #eb5757;
    margin-right: 7px;
  }
  .card {
    width: min-content;
  }
  section {
    display: flex;
    justify-content: space-between;
  }
  .body-host {
    font-weight: 700;
    margin-right: 11px;
    margin-top: 15px;
    font-size: 12px;
    line-height: 15px;
    text-transform: uppercase;
    color: #4f4f4f;
    border: 1px solid #4f4f4f;
    box-sizing: border-box;
    border-radius: 12px;
    padding: 7px 10px;
  }
  .body-content {
    margin-top: 21px;
    font-size: 12px;
  }
  .body-rating {
    margin-top: 21px;
  }
  .title {
    font-size: 16px;
    line-height: 20px;
    font-weight: 600;
  }
  .body {
    display: flex;
  }
  .card-title {
    margin-top: 12px;
    font-size: 16px;
    line-height: 20px;
    color: #333333;
    font-weight: 600;
  }
}
@media screen and (max-width: 375px) {
  img {
    height: 238px;
    width: 350px;
    border-radius: 24px;
  }
  p {
    font-size: 14px;
    line-height: 17px;
    color: #828282;
  }
  .star {
    font-size: 16px;
    color: #eb5757;
    margin-right: 7px;
  }
  .card {
    width: min-content;
    padding: 0px 12px 32px 12px;
  }
  section {
    display: flex;
    justify-content: space-between;
  }
  .body-host {
    font-weight: 700;
    margin-right: 11px;
    margin-top: 15px;
    font-size: 10px;
    line-height: 14px;
    text-transform: uppercase;
    color: #4f4f4f;
    border: 1px solid #4f4f4f;
    box-sizing: border-box;
    border-radius: 12px;
    padding: 7px 10px;
  }
  .body-content {
    margin-top: 21px;
  }
  .body-rating {
    margin-top: 21px;
  }
  .title {
    font-size: 16px;
    line-height: 20px;
    font-weight: 600;
  }
  .body {
    display: flex;
  }
  .card-title {
    margin-top: 12px;
    font-size: 16px;
    line-height: 20px;
    color: #333333;
    font-weight: 600;
  }
}
</style>
