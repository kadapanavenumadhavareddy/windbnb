<template>
  <div class="filter-drawer">
    <div class="filter-body">
      <div class="sm">
        <div>Edit your search</div>
        <Button
          buttonstyle="removedefault"
          @clicked="
            () => {
              $emit('filterdraweroff');
            }
          "
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="20"
            viewBox="0 0 48 48"
            width="20"
          >
            <path
              d="M38 12.83l-2.83-2.83-11.17 11.17-11.17-11.17-2.83 2.83 11.17 11.17-11.17 11.17 2.83 2.83 11.17-11.17 11.17 11.17 2.83-2.83-11.17-11.17z"
            />
            <path d="M0 0h48v48h-48z" fill="none" /></svg
        ></Button>
      </div>
      <div class="filter-body-cont flex">
        <div
          class="filter-content"
          :class="[active == 'location' ? 'active' : '']"
          @click="check('location')"
        >
          <div>Location</div>
          <div class="sub">
            {{ selectedlocation.city }}, {{ selectedlocation.country }}
          </div>
        </div>
        <div
          class="filter-content"
          :class="[active == 'guest' ? 'active' : '']"
          @click="check('guest')"
        >
          <div>Guests</div>
          <div class="sub">Add Guests</div>
        </div>
        <div
          style="
            width: 30%;
            display: flex;
            justify-content: center;
            color: #ffffff;
          "
          class="large"
        >
          <Button
            fillcolor="#ffffff"
            buttonstyle="search-button"
            :icon="true"
            @clicked="search()"
            >Search</Button
          >
        </div>
      </div>
      <div v-if="active == 'location'">
        <div v-for="loc in $store.state.places" :key="loc">
          <p class="place" @click="selected(loc.city, loc.country)">
            <span class="material-icons">place</span>{{ loc.city }},
            {{ loc.country }}
          </p>
        </div>
      </div>

      <div v-else>
        <div style="margin-left: 49px">
          <div class="adult">
            <p style="font-weight: 700; color: black">Adults</p>
            <p>Ages 13 or above</p>
            <div style="display: flex; margin-top: 12px">
              <Button @clicked="decrement('adult')">-</Button>
              <p style="margin: 0px 10px 0px 10px">{{ adults }}</p>
              <Button @clicked="increment('adult')">+</Button>
            </div>
          </div>
          <div class="children">
            <p style="font-weight: 700; color: black">Children</p>
            <p>Age 2-12</p>
            <div style="display: flex; margin-top: 12px">
              <Button @clicked="decrement('child')">-</Button>
              <p style="margin: 0px 10px 0px 10px">{{ childrens }}</p>
              <Button @clicked="increment('child')">+</Button>
            </div>
          </div>
        </div>
      </div>
      <div
        style="
          width: 100%;
          display: flex;
          justify-content: center;
          color: #ffffff;
        "
        class="small"
      >
        <Button
          fillcolor="#ffffff"
          buttonstyle="search-button"
          :icon="true"
          @clicked="search()"
          >Search</Button
        >
      </div>
    </div>
  </div>
</template>
<script scoped>
import Button from "./ButtonComponent.vue";
export default {
  props: ["tab"],
  emits: ["filterdraweroff"],
  components: {
    Button,
  },
  data() {
    return {
      active: "location",
      selectedlocation: { city: "Helsinki", country: "Finland" },
      adults: 0,
      childrens: 0,
    };
  },
  methods: {
    check(val) {
      this.active = val;
    },
    selected(city, country) {
      this.selectedlocation = { city: city, country: country };
    },
    increment(val) {
      if (val == "child") {
        this.childrens++;
      } else {
        this.adults++;
      }
    },
    decrement(val) {
      if (val == "child") {
        this.childrens -= this.childrens == 0 ? 0 : 1;
      } else {
        this.adults -= this.adults == 0 ? 0 : 1;
      }
    },
    search() {
      this.$store.dispatch("search", {
        adults: this.adults,
        childrens: this.childrens,
        city: this.selectedlocation.city,
        country: this.selectedlocation.country,
      });
      this.$store.commit("selceted", this.selectedlocation);
      this.$emit("filterdraweroff");
    },
  },
  created() {
    this.active = this.tab;
    this.selectedlocation =
      this.$store.state.selectedplace == null
        ? this.$store.state.places[0]
        : this.$store.state.selectedplace;
  },
};
</script>
