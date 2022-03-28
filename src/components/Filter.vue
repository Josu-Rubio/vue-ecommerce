<script>
export default {
  name: 'Filter',
  props: {
    brands: { type: Array },
    departments: { type: Array },
    seen: { type: Boolean },
    searchItems: { type: Array },
  },
};
</script>

<template>
  <div>
    <button @click="brandSeen = !brandSeen" class="buttonFilter">
      Marca &#8626;
    </button>
    <form class="filter" action="" v-if="brandSeen">
      <div>
        <input type="radio" @click="$emit('filterBy', '')" />
        <label for="">ALL</label>
      </div>
      <div v-for="brand of brands" :key="brand.id">
        <input
          type="radio"
          @click="$emit('filterBy', { brand })"
          value="{{brand}}"
        />
        <label for="{{ brand }}">{{ brand }}</label>
      </div>
    </form>
    <button @click="deptSeen = !deptSeen" class="buttonFilter">
      Departamento &#8626;
    </button>
    <form class="filter" action="" v-if="deptSeen">
      <div>
        <input type="radio" @click="$emit('filterBy', '')" />
        <label for="">ALL</label>
      </div>
      <div v-for="department of departments" :key="department.id">
        <input type="radio" @click="$emit('filterBy', { department })" />
        <label>{{ department }}</label>
      </div>
    </form>
  </div>
</template>

<style></style>
