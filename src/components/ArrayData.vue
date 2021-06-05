<template>
  <div :class="name" :title="subtitle">
    <span v-bind:key="a" v-for="a in bangumi[name]">
      <auto-input v-on:submit="update" :val="a"></auto-input>
    </span>
    <button v-on:click="add">+</button>
  </div>
</template>

<script>
import AutoInput from "./AutoInput.vue";

export default {
  name: "array-data",
  components: {
    AutoInput,
  },
  props: ["bangumi", "name", "title"],
  computed: {
    subtitle: function () {
      if (this.title == null) {
        return this.name + ": ";
      } else {
        return this.title + ": ";
      }
    },
  },
  methods: {
    update: function (orival, val) {
      if (val == "" || val == null) {
        this.$emit("remove", this.bangumi.ID, this.name, orival);
      } else {
        this.$emit("submit", this.bangumi.ID, this.name, orival, val);
      }
    },
    add: function () {
      var newval = prompt("New " + this.name);
      if (newval) {
        this.$emit("invert", this.bangumi.ID, this.name, newval);
      }
    },
  },
};
</script>

<style scoped>
::before {
  content: attr(title);
  font-weight: bold;
}

span + span::before {
  content: ",";
}
</style>