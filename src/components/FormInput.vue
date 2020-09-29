<template>
  <div id="formInput">
    <div>{{ text }}:</div>
    <div>
      <input :name="name" type="text" required />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    text: String,
  },
};
</script>

<style scoped>
#formInput {
  display: flex;
  margin-bottom: 1rem;
}
#formInput div:first-child {
  width: 30%;
}
#formInput div:last-child {
  width: 70%;
  display: contents;
}
input {
  width: 100%;
  outline: none;
}
</style>