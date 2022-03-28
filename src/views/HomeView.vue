<script>
// import Filter from '../components/Filter.vue';  --> Working on component
// import Items from '../components/Items.vue';  --> Working on component

import axios from 'axios';

//We created a new API because of CORS policy reasons
const URL = 'https://mocki.io/v1/e382be53-e13a-4d06-a883-32ecffd0eef1';
const decathlonURL = 'https://www.decathlon.es/static/training/data.json';

export default {
  name: 'home',
  data() {
    return {
      items: [],
      brands: [],
      departments: [],
      searchItem: [],
      brandSeen: false,
      deptSeen: false,
    };
  },
  // Components doesn't work
  //
  // components: {
  //   Filter,
  //   Items,
  // },
  async created() {
    try {
      const res = await axios.get(URL);
      this.items = res.data.data.data.blocks.items;
      for (let i = 0; i < this.items.length; i++) {
        this.brands.indexOf(this.items[i].brand.label) === -1
          ? this.brands.push(this.items[i].brand.label)
          : '';

        this.departments.indexOf(this.items[i].departmentLabel) === -1
          ? this.departments.push(this.items[i].departmentLabel)
          : '';
      }
    } catch (e) {
      console.error(e);
    }
  },
  //This was thought for the Item Component. Shouldn't be here
  //
  computed: {
    searchItems() {
      const filteredItems = [];
      const search = this.searchItem;

      if (!search) {
        return this.items;
      } else {
        for (let i = 0; i < this.items.length; i++) {
          this.items[i].brand.label.includes(search) ||
          this.items[i].departmentLabel.includes(search)
            ? filteredItems.push(this.items[i])
            : '';
        }
        return filteredItems;
      }
    },
  },
  // This Method doesn't work It's thought for Filter Component
  //
  // methods: {
  //   filterBy(n) {
  //     this.searchItem = n;
  //   },
  // },
};
</script>

<template>
  <div class="bodyWrapper">
    <aside>
      <div class="asideHeader">
        <img src="../assets/img/filters.png" alt="" />
        <p>Filtros</p>
      </div>

      <!-- Create Filter Component -->
      <button @click="brandSeen = !brandSeen" class="buttonFilter">
        Marca &#8626;
      </button>
      <form class="filter" action="" v-if="brandSeen">
        <div>
          <input type="radio" @click="searchItem = ''" />
          <label for="">ALL</label>
        </div>
        <div v-for="brand of brands" :key="brand.id">
          <input type="radio" @click="searchItem = brand" value="{{brand}}" />
          <label for="{{ brand }}">{{ brand }}</label>
        </div>
      </form>
      <button @click="deptSeen = !deptSeen" class="buttonFilter">
        Deporte &#8626;
      </button>
      <form class="filter" action="" v-if="deptSeen">
        <div>
          <input type="radio" @click="searchItem = ''" />
          <label for="">ALL</label>
        </div>
        <div v-for="department of departments" :key="department.id">
          <input type="radio" @click="searchItem = department" />
          <label>{{ department }}</label>
        </div>
      </form>
      <!--  -->
      <!-- <Filter v-bind:brands="brands" v-bind:department="department" v-bind:seen="seen" @filter-by="filterBy" /> -->
    </aside>

    <main>
      <!-- Create an ITEMS component -->
      <div id="items" class="items" v-for="item of searchItems" :key="item.id">
        <div class="itemWrapper">
          <div class="itemTop">
            <img :src="item.models[0].image.url" alt="" />
            <span class="itemPrice">€ {{ item.models[0].price }}</span>
          </div>

          <div class="itemBottom">
            <p>{{ item.brand.label }}</p>
            <p>{{ item.webLabel }}</p>
          </div>
        </div>
      </div>
      <!--  -->
      <!-- <Items v-bidn:items="items" v-bind:searchItem="searchItem" /> -->
    </main>
  </div>
</template>

<style>
@import '@/assets/homeview.scss';
</style>
