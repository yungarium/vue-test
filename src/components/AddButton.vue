<template>
  <div>
    <button @click="openModal">Добавить</button>
  </div>
</template>

<script>
export default {
  methods: {
    openModal() {
      this.$emit("openModal", true);
    },
  },
};
</script>

<style scoped>
div {
  width: 70%;
  display: flex;
  justify-content: flex-end;
  margin-bottom: 1.5rem;
}
button {
  border: 2px solid black;
  border-radius: 1rem;
  padding: 1rem 1.5rem;
  font-size: 1.2rem;
  cursor: pointer;
  outline: none;
}
button:hover {
  background-color: rgb(185, 255, 185);
}
</style>