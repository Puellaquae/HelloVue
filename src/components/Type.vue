<template>
  <div class="Type" :title="subtitle">
    <select v-on:change="select" v-model="val">
      <option v-bind:key="type" v-for="type in Types">{{ type }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "type",
  props: ["bangumi", "title"],
  data() {
    return {
      val: this.bangumi.Type,
      orival: this.bangumi.Type,
      Types: ["TV", "MOVIE", "OVA", "SP", "LIVE"],
    };
  },
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
    select: function () {
      this.$emit("submit", this.bangumi.ID, "Type", this.orival, this.val);
      this.orival = this.val;
    },
  },
};
</script>

<style scoped>
::before {
  content: attr(title);
  font-weight: bold;
}

* {
    border: none;
    font-size: 1rem;
}
</style>