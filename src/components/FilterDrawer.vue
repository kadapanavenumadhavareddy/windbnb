<template>
  <div class="filter-drawer">
    <div class="filter-body">
      <div class="filter-body-cont">
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
          <button class="searchfilter" style="color: #ffffff" @click="search">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              x="0px"
              y="0px"
              width="10"
              height="10"
              viewBox="0 0 30 30"
              style="fill: #ffffff; margin-right: 10px"
            >
              <path
                d="M 13 3 C 7.4889971 3 3 7.4889971 3 13 C 3 18.511003 7.4889971 23 13 23 C 15.396508 23 17.597385 22.148986 19.322266 20.736328 L 25.292969 26.707031 A 1.0001 1.0001 0 1 0 26.707031 25.292969 L 20.736328 19.322266 C 22.148986 17.597385 23 15.396508 23 13 C 23 7.4889971 18.511003 3 13 3 z M 13 5 C 17.430123 5 21 8.5698774 21 13 C 21 17.430123 17.430123 21 13 21 C 8.5698774 21 5 17.430123 5 13 C 5 8.5698774 8.5698774 5 13 5 z"
              ></path>
            </svg>
            Search
          </button>
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
              <button
                class="btn"
                style="margin-right: 10px"
                @click="decrement('adult')"
              >
                -
              </button>
              <p>{{ adults }}</p>
              <button
                class="btn"
                style="margin-left: 10px"
                @click="increment('adult')"
              >
                +
              </button>
            </div>
          </div>
          <div class="children">
            <p style="font-weight: 700; color: black">Children</p>
            <p>Age 2-12</p>
            <div style="display: flex; margin-top: 12px">
              <button
                class="btn"
                style="margin-right: 10px"
                @click="decrement('child')"
              >
                -
              </button>
              <p>{{ childrens }}</p>
              <button
                class="btn"
                style="margin-left: 10px"
                @click="increment('child')"
              >
                +
              </button>
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
        <button class="searchfilter" style="color: #ffffff" @click="search">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            x="0px"
            y="0px"
            width="10"
            height="10"
            viewBox="0 0 30 30"
            style="fill: #ffffff; margin-right: 10px"
          >
            <path
              d="M 13 3 C 7.4889971 3 3 7.4889971 3 13 C 3 18.511003 7.4889971 23 13 23 C 15.396508 23 17.597385 22.148986 19.322266 20.736328 L 25.292969 26.707031 A 1.0001 1.0001 0 1 0 26.707031 25.292969 L 20.736328 19.322266 C 22.148986 17.597385 23 15.396508 23 13 C 23 7.4889971 18.511003 3 13 3 z M 13 5 C 17.430123 5 21 8.5698774 21 13 C 21 17.430123 17.430123 21 13 21 C 8.5698774 21 5 17.430123 5 13 C 5 8.5698774 8.5698774 5 13 5 z"
            ></path>
          </svg>
          Search
        </button>
      </div>
    </div>
  </div>
</template>
<script scoped>
export default {
  props: ["tab"],
  emits: ["filterdraweroff"],
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
  mounted() {
    this.active = this.tab;
  },
};
</script>
<style>
* {
  margin: 0px;
  padding: 0px;
}
.place {
  cursor: pointer;
}
@media screen and (max-width: 375px) {
  .small {
    display: block;
    margin-top: 182px;
  }
  .large {
    display: none !important;
  }
  .filter-drawer {
    background: rgba(79, 79, 79, 0.4);
    width: 100%;
    height: 170vh;
    position: absolute;
    top: 0px;
    left: 0px;
  }
  .filter-body {
    margin: auto;
    background-color: #ffffff;
    width: 100%;
  }
  .filter-body-cont {
    display: flex;
    flex-direction: column;
    box-shadow: 0px 1px 6px 0px black;
    border-radius: 16px;
    width: 350px;
    margin-left: 12px;
  }
  .filter-content {
    width: 100%;
  }
  .material-icons {
    width: 14px;
    height: 19px;
    margin-right: 10px;
    margin-left: 49px;
    color: #333333;
  }
  .place {
    margin-top: 36px;
  }
  .active {
    border-radius: 16px;
  }
  .filter-content {
    padding: 12px 26px;
    cursor: pointer;
  }
  .btn {
    height: 23px;
    width: 23px;
    padding: 7px;
    border-radius: 4px;
    box-sizing: border-box;
    border: 1px solid #333333;
    font-size: 9px;
  }
  .adult {
    margin-top: 48px;
  }
  .children {
    margin-top: 52px;
  }
  .searchfilter {
    height: 48px;
    width: 126px;
    background-color: rgba(235, 87, 87, 0.9);
    border: none;
    border-radius: 16px;
    margin: 6px 0px;
  }
  .sub {
    color: #bdbdbd;
  }
  .active .sub {
    color: black;
  }
}
@media screen and (min-width: 1020px) {
  .large {
    display: block;
  }
  .small {
    display: none !important;
  }
  .filter-drawer {
    background: rgba(79, 79, 79, 0.4);
    width: 100%;
    height: 170vh;
    position: absolute;
    top: 0px;
    left: 0px;
  }
  .filter-body {
    padding: 90px 10%;

    margin: auto;

    background-color: #ffffff;
  }
  .filter-body-cont {
    display: flex;
    box-shadow: 0px 1px 6px 0px black;
    border-radius: 16px;
  }
  .filter-content {
    width: 30%;
  }
  .material-icons {
    width: 14px;
    height: 19px;
    margin-right: 10px;
    color: #333333;
  }
  .place {
    margin-top: 36px;
  }
  .active {
    border-radius: 16px;
    border: 1px solid #333333;
  }
  .filter-content {
    padding: 12px 26px;
    cursor: pointer;
    /* box-shadow: 0px 1px 6px 0px black; */
  }
  .btn {
    height: 23px;
    width: 23px;
    padding: 7px;
    border-radius: 4px;
    box-sizing: border-box;
    border: 1px solid #333333;
    font-size: 9px;
  }
  .adult {
    margin-top: 48px;
  }
  .children {
    margin-top: 52px;
  }
  .searchfilter {
    height: 48px;
    width: 126px;
    background-color: rgba(235, 87, 87, 0.9);
    border: none;
    border-radius: 16px;
    margin: 6px 0px;
  }
  .sub {
    color: #bdbdbd;
  }
  .active .sub {
    color: black;
  }
}
</style>
