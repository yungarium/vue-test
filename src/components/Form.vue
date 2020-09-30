<template>
  <form
    id="tableWrapper"
    :class="toggleFunc()"
    @submit="onSave"
    autocomplete="off"
  >
    <div>
      <h3>Добавление нового пользователя</h3>
      <div id="closeBtn" @click="closeModal">x</div>
    </div>
    <div id="tableBody">
      <FormInput name="name" text="Имя" />
      <FormInput name="phone" text="Телефон" />
      <FormSelect name="chief" text="Начальник" :allPeople="data" />
    </div>
    <div>
      <SaveButton />
    </div>
  </form>
</template>

<script>
import FormInput from "./FormInput";
import FormSelect from "./FormSelect";
import SaveButton from "./SaveButton";
export default {
  props: {
    isActive: Boolean,
    data: Array,
  },
  components: {
    FormInput,
    FormSelect,
    SaveButton,
  },
  methods: {
    toggleFunc() {
      return {
        active: this.isActive,
      };
    },
    closeModal() {
      this.$emit("openModal", false);
    },
    onSave(e) {
      e.preventDefault();

      const form = e.target;
      const formData = new FormData(form);
      let newPerson = {};

      for (const [inputName, value] of formData) {
        if (inputName == "name") newPerson.name = value;
        if (inputName == "phone") newPerson.phone = value;
        if (inputName == "chief") newPerson.chief = value;
      }

      newPerson.children = [];

      this.$emit("onSubmit", newPerson);
      event.target.reset();
    },
  },
};
</script>

<style scoped>
#tableWrapper {
  display: none;
  position: relative;
  background-color: white;
  padding: 1.5rem;
  border: 2px solid black;
  width: 70%;
  box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.75);
}
#tableBody {
  margin-top: 2rem;
}
#closeBtn {
  position: absolute;
  padding: 1rem;
  cursor: pointer;
  right: 0;
  top: 0;
}
#closeBtn:hover {
  text-decoration: underline;
}
.active {
  display: block !important;
}
</style>