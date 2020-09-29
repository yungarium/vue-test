<template>
  <div id="formSelect">
    <div>{{ text }}:</div>
    <div>
      <select :name="name">
        <option selected value></option>
        <option v-for="(man, index) in allPeople" :key="index">
          {{ man.name }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    text: String,
    allPeople: Array,
  },
};
</script>

<style scoped>
#formSelect {
  display: flex;
  margin-bottom: 1rem;
}
#formSelect div:first-child {
  width: 30%;
}
#formSelect div:last-child {
  width: 70%;
  display: contents;
}
select {
  width: 100%;
  outline: none;
}
</style>