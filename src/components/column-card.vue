<template>
  <div class="row col-5 gap-1">
  <div
    v-for="(country, index) in countries"
    :key="country['id']"
    :class="['column-card', { 'column-check': activeCountry === index }]" 
    @click.prevent="clickable(index)"
  >
    <span id="column-tip">show its businesses</span>

    <div class="column-card-first column-card-state">
      <img :src="country['img']" :alt="country['name']" />
      <span>{{ country["nationality"] }}</span>
    </div>

    <span id="of">of</span>

    <div class="column-card-second column-card-state">
      <img :src="country['img_second']" :alt="country['name_second']" />
      <span>{{ country["nationality_second"] }}</span>
    </div>
  </div>
</div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "vue-property-decorator";

@Component({ name: "column-card" })
export default class ColumnCard extends Vue {
  @Prop() countries;
  activeCountry = null;

  clickable(index) {
    console.log(this.activeCountry)
    console.log(index)
    this.activeCountry !== index ? 
      this.activeCountry = index :
      this.activeCountry = null;
  }
}
</script>


<style lang="scss" scoped>
.column-check {
  background-color: #46ad91 !important;
  box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.7);
  border-color: #46ad91 !important;

  span {
    color: white !important;
  }
}

.column-card {

  &-wrapper {
    display: grid;
    align-content: center;
    align-items: center;
  }

  padding: 0.6rem 1rem;
  margin-bottom: 2rem;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  border-radius: 0.3rem;
  width: 100%;
  position: relative;
  transition: all 0.5s ease;
  cursor: pointer;

  background-color: #f2eeec;
  border-radius: 6px;
  border: 1px solid #bdbdbd;

  &:hover {
    background-color: #46ad91;
    box-shadow: 0px 1px 10px rgba($color: #000000, $alpha: 0.7);
    border-color: #46ad91;
  }
  &:hover span {
    color: white;
  }
  &:hover #column-tip {
    opacity: 1;
  }
  img {
    height: 2rem;
    width: 3rem;
  }

  span {
    display: block;
    margin: {
      top: 0.5rem;
    }
    font-size: 0.8rem;
    text-transform: uppercase;
    color: #333;
  }
}
#column-tip {
  color: #46ad91;
  font-weight: 500;
  font-size: 0.7rem;
  position: absolute;
  bottom: -1.2rem;
  left: 1.3rem;
  opacity: 0;
  transition: all 0.4s ease;
}
.column-card-state {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 6rem;
}
#of {
  margin: 0rem 1rem;
}

@media (max-width: 991px) {
  .column-card-state {
    width: 5.6rem;
    padding: 0.3rem 0rem;
  }
  #of‌ {
    margin: 0rem;
  }

  .column-card {
    span {
      margin: 0rem 0.3rem;
      font-size: 0.6rem;
    }
    img {
      height: 1rem;
      width: 2rem;
    }
  }
}
@media (max-width: 575px) {
  .column-card {
    span {
      margin: 0rem 0.3rem;
      font-size: 0.6rem;
    }
    img {
      height: 2rem;
      width: 3rem;
      margin-bottom: 0.6rem;
    }
  }
  .column-card-state {
    width: 1rem;
  }
}
</style>