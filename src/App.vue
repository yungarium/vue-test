<template>
  <div id="app">
    <div class="block">
      <AddButton @openModal="omFunc" />
      <Table :data="peopleArr" />
    </div>
    <div class="block">
      <Form
        :isActive="show"
        @openModal="omFunc"
        @onSubmit="onSubmitForm"
        :data="peopleNamesArr"
      />
    </div>
  </div>
</template>

<script>
import AddButton from "./components/AddButton";
import Table from "./components/Table";
import Form from "./components/Form";
export default {
  name: "App",
  components: {
    AddButton,
    Table,
    Form,
  },
  methods: {
    omFunc(data) {
      this.show = data;
    },
    onSubmitForm(arr) {
      // проверяем есть ли шеф
      if (arr[0].chief) {
        // находим индекс по имени
        let insertAtIndex = this.peopleArr.findIndex(
          (x) => x.name === arr[0].chief
        );
        this.peopleArr[insertAtIndex].children.push(arr);
        console.log(this.peopleArr[insertAtIndex]);
      } else {
        // если нет шефа просто добавляем в конец
        this.peopleArr = this.peopleArr.concat(arr);
      }

      this.getNames();
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      const parsed = JSON.stringify(this.peopleArr);
      localStorage.setItem("peopleArr", parsed);
    },
    getNames() {
      this.peopleNamesArr = this.peopleArr.filter(function (item) {
        return item.name;
      });
    },
  },
  data() {
    return {
      show: false,
      peopleArr: [],
      peopleNamesArr: [],
    };
  },
  mounted() {
    if (localStorage.getItem("peopleArr")) {
      try {
        this.peopleArr = JSON.parse(localStorage.getItem("peopleArr"));
        this.getNames();
      } catch (e) {
        localStorage.removeItem("peopleArr");
      }
    }
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  font-family: "Roboto", sans-serif;
}
#app {
  height: 100vh;
  display: flex;
  background: url("./assets/images/background.png");
}
.block {
  width: 50%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}
</style>
