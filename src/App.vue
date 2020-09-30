<template>
  <div id="app">
    <div class="block">
      <AddButton @openModal="isModalOpen" />
      <Table :data="people" />
    </div>
    <div class="block">
      <Form
        :isActive="show"
        @openModal="isModalOpen"
        @onSubmit="onSubmitForm"
        :data="peopleNames"
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
    isModalOpen(data) {
      this.show = data;
    },
    onSubmitForm(newPerson) {
      if (newPerson.chief) {
        let insertAtIndex = this.people.findIndex(
          (x) => x.name === newPerson.chief
        );
        this.people[insertAtIndex].children.push(newPerson);
      } else {
        this.people.push(newPerson);
      }

      this.getNames();
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      const parsed = JSON.stringify(this.people);
      localStorage.setItem("people", parsed);
    },
    getNames() {
      this.peopleNames = this.people.filter(function (item) {
        return item.name;
      });
    },
  },
  data() {
    return {
      show: false,
      people: [],
      peopleNames: [],
    };
  },
  mounted() {
    if (localStorage.getItem("people")) {
      try {
        this.people = JSON.parse(localStorage.getItem("people"));
        this.getNames();
      } catch (e) {
        localStorage.removeItem("people");
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
