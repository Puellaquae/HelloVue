<template>
  <div :class="name" :title="subtitle">
    <auto-input v-on:submit="submit" :check="check" :val="bangumi[name]" />
  </div>
</template>

<script>
import AutoInput from "./AutoInput.vue";

export default {
  name: "mono-data",
  components: {
    AutoInput,
  },
  props: ["bangumi", "name", "check", "title"],
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
    submit: function (orival, val) {
      this.$emit("submit", this.bangumi.ID, this.name, orival, val);
    },
  },
};
</script>

<style scoped>
::before {
  content: attr(title);
  font-weight: bold;
}
</style>