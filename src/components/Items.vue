<script>
export default {
  name: 'Items',
  props: {
    items: {
      type: Array,
    },
    searchItem: {
      type: Array,
    },
  },
  computed: {
    searchItems() {
      const filteredItems = [];
      const search = this.searchItem;

      console.log(this.items);

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
};
</script>

<template>
  <div>
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
  </div>
</template>

<style></style>
