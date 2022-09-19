<template>
  <div>
    <input
      type="text"
      class="form-control"
      placeholder="Neue Aufgabe"
      v-model="content"
    />
    <small>Noch {{ numberOfCharsLeft }} Zeichen erlaubt</small>
    <div class="d-grid my-2">
      <button class="btn btn-secondary" @click="submitTask()">Eintragen</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  emits: {
    "new-task": (task) => {
      if (task.content === "") {
        console.warn("NewTaskComponent: Der Content sollte nicht leer sein.");
        return false;
      }
      return true;
    },
  },
  inject: ["maxNumberOfChars"],
  data() {
    return {
      content: "",
    };
  },
  methods: {
    submitTask() {
      this.$emit("new-task", {
        content: this.content,
      });
      this.content = "";
    },
  },
  computed: {
    numberOfCharsLeft() {
      return this.maxNumberOfChars - this.content.length;
    },
  },
};
</script>

<style scoped></style>
