<template>
  <li>
    <div id="tableItem" @click="toggle" :class="{ cursorPointer: isFolder }">
      <div>
        <span v-if="isFolder">[{{ open ? "-" : "+" }}]</span>
        {{ data.name }}
      </div>
      <div>{{ data.phone }}</div>
    </div>

    <ul v-show="open">
      <TableItemNode
        v-for="(item, index) in data.children"
        :key="index"
        :data="item[index]"
      />
    </ul>
  </li>
</template>

<script>
export default {
  name: "TableItemNode",
  props: {
    data: Object,
  },
  data() {
    return {
      open: false,
    };
  },
  methods: {
    toggle() {
      this.open = !this.open;
    },
  },
  computed: {
    isFolder: function () {
      return this.data.children && this.data.children.length;
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
#tableItem {
  display: flex;
}
#tableItem div {
  width: 50%;
  padding: 0.8rem 1rem;
  border: 2px solid black;
  border-top: 0;
}
#tableItem div:first-child {
  border-right: 0;
}
.cursorPointer {
  cursor: pointer;
}
li {
  list-style: none;
}
ul #tableItem div {
  padding-left: 2rem;
}
</style>