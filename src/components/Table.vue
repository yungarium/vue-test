<template>
  <div id="tableWrapper">
    <div id="tableHeader">
      <div v-on:click="sortBy('name')">Имя</div>
      <div v-on:click="sortBy('phone')">Телефон</div>
    </div>
    <div id="tableBody">
      <TableItem v-for="(item, index) in data" :key="index" :data="item" />
    </div>
  </div>
</template>

<script>
import TableItem from "./TableItem";
export default {
  props: {
    data: Array,
  },
  components: {
    TableItem,
  },
  methods: {
    sortBy(option) {
      let i;
      function compare(a, b) {
        if (option == "name")
          a.name < b.name ? (i = -1) : a.name > b.name ? (i = 1) : (i = 0);
        else
          a.phone < b.phone ? (i = -1) : a.phone > b.phone ? (i = 1) : (i = 0);
        return i;
      }

      return this.data.sort(compare);
    },
  },
};
</script>

<style scoped>
button {
  border: 2px solid black;
  border-radius: 1rem;
  padding: 1rem 2rem;
  font-size: 1.5rem;
  cursor: pointer;
  outline: none;
}
button:hover {
  background-color: rgb(185, 255, 185);
}
#tableWrapper {
  width: 70%;
  background-color: white;
  box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.75);
}
#tableHeader {
  display: flex;
  width: 100%;
  font-weight: bold;
}
#tableHeader div {
  width: 50%;
  cursor: pointer;
  padding: 0.8rem 1rem;
  border: 2px solid black;
}
#tableHeader div:hover {
  background-color: rgb(167, 167, 167);
}
#tableHeader div:first-child {
  border-right: 0;
}
</style>