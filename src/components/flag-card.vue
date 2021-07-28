<template>
  <div class="flag-card-wrapper">
    <div
      v-for="(country, index) in countries" :key="country['id']"
      @click.prevent="clickable(index)"
    >
      <div :class="['flag-card', { 'flag-check': activeCountry === index }]">
        <img :src="country.img" :alt="country" />
        <span class="check" v-if="activeCountry === index"><i class="gg-check"></i></span>

        <span class="name">{{ country.nationality }}</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component({ name: "flag-card" })
export default class FlagCard extends Vue {
  @Prop() countries;
  activeCountry = null;

  clickable(index) {
    this.activeCountry !== index ? 
      this.activeCountry = index :
      this.activeCountry = null;
  }
}
</script>


<style lang="scss" scoped>
.flag-check {
  background-color: #46ad91;
  box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.7);
  position: absolute;

  span {
    color: white !important;
  }
}
.flag-card {
  padding: 0.6rem 1rem;
  display: flex;
  flex-direction: column;
  border-radius: 0.3rem;
  width: 6.7rem;
  position: relative;
  transition: all 0.5s ease;
  cursor: pointer;
  &:hover {
    background-color: #46ad91;
    box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.7);
  }
  &:hover span {
    color: white;
  }
  img {
    height: 2rem;
    width: 3rem;
  }

  span {
    display: block;
    font-size: 0.8rem;
    text-transform: uppercase;
    color: #333;
  }

  .check {
    position: absolute;
    right: 0rem;
    top: 0rem;
    color: white;
  }

  .name {
  margin-top: 0.5rem;
  }
}

.flag-card-wrapper {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 2rem 3rem;
  margin: 3rem auto 2rem;
}
@media (max-width: 991px) {
  .flag-card-wrapper {
    grid-template-columns: repeat(3, auto);
    gap: 0.2rem 0rem;
  }
}
@media (max-width: 575px) {
  .flag-card-wrapper {
    grid-template-columns: repeat(2, auto);
    gap: 0.2rem 0rem;
  }
}
</style>