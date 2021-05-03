<template>
  <div class="todo">
    <h3>{{ title }}</h3>
    <div id="util">
      <input
        type="checkbox"
        id="checkbox"
        @click="toggleFinished"
        @input="toggleFinished"
        v-if="finished"
        checked
      />
      <input type="checkbox" id="checkbox" @click="toggleFinished" v-else />
      <button @click="deleteTodo">X</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["title", "finished", "id"],
  methods: {
    deleteTodo() {
      this.$emit("deleteTodo", this.id);
    },
    toggleFinished() {
      this.$emit("toggleFinished", this.id);
    },
  },
};
</script>

<style>
.todo {
  background-color: #2c3e50;
  color: white;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  flex-direction: row;
  width: 400px;
  height: 50px;
  padding: 2px;
  border-radius: 15px;
  margin: 10px;
  height: 3em;
}
.todo h3 {
  margin: auto 0;
  margin-left: 10px;
}
.todo #util {
  margin: auto 0;
  margin-right: 10px;
}
.todo button {
  color: #2c3e50;
  background: white;
  border-radius: 100px;
  width: 2em;
  height: 2em;
  text-align: center;
  border: none;
}
.todo input {
  width: 1em;
  height: 1em;
}
</style>