<template>
  <div v-bind:key="bang.ID" v-for="bang in Bangumis" class="Bangumi">
    <b>ID: {{ bang.ID }}</b>
    <mono-data :bangumi="bang" :name="'Name'" v-on:submit="Update" />
    <array-data
      :bangumi="bang"
      :name="'Alias'"
      v-on:submit="Update"
      v-on:invert="Invert"
      v-on:remove="Remove"
    />
    <type :bangumi="bang" :title="'Type'" v-on:submit="Update" />
    <array-data
      :bangumi="bang"
      :name="'Studios'"
      v-on:submit="Update"
      v-on:invert="Invert"
      v-on:remove="Remove"
    />
    <array-data
      :bangumi="bang"
      :name="'CoSubs'"
      :title="'First Part Subtitles'"
      v-on:submit="Update"
      v-on:invert="Invert"
      v-on:remove="Remove"
    />
    <array-data
      :bangumi="bang"
      :name="'TPSubs'"
      :title="'Third Part Subtitles'"
      v-on:submit="Update"
      v-on:invert="Invert"
      v-on:remove="Remove"
    />
    <mono-data
      :bangumi="bang"
      :name="'ReleaseDate'"
      :title="'Release Date'"
      v-on:submit="Update"
      :check="CheckDate"
    />
    <array-data
      :bangumi="bang"
      :name="'Patches'"
      v-on:submit="Update"
      v-on:invert="Invert"
      v-on:remove="Remove"
    />
    <mono-data :bangumi="bang" :name="'Set'" v-on:submit="Update" />
  </div>
  <button v-on:click="RemoveBangumi">Remove Bangumi</button>
  <button v-on:click="AddBangumi">Add New Bangumi</button>
</template>

<script>
import Type from "./Type.vue";
import ArrayData from "./ArrayData.vue";
import MonoData from "./MonoData.vue";

export default {
  name: "bangumis",
  components: {
    Type,
    ArrayData,
    MonoData,
  },
  data() {
    return {
      NewContent: "",
      Bangumis: [
        {
          ID: "id",
          Name: "Name",
          Alias: ["Alias"],
          Type: "TV",
          Studios: ["Studio"],
          CoSubs: ["CoSubs"],
          TPSubs: ["TPSubs"],
          ReleaseDate: "20-20-20",
          Patches: ["Patch"],
          Set: "Set",
        },
      ],
    };
  },
  methods: {
    Update: function (bid, name, orival, newval) {
      for (let index = 0; index < this.Bangumis.length; index++) {
        if (this.Bangumis[index].ID == bid) {
          if (typeof this.Bangumis[index][name] != typeof orival) {
            for (let i = 0; i < this.Bangumis[index][name].length; i++) {
              if (this.Bangumis[index][name][i] == orival) {
                this.Bangumis[index][name][i] = newval;
              }
            }
          } else if (this.Bangumis[index][name] == orival) {
            this.Bangumis[index][name] = newval;
          }
        }
      }
    },
    Invert: function (bid, name, newval) {
      for (let index = 0; index < this.Bangumis.length; index++) {
        if (this.Bangumis[index].ID == bid) {
          if (typeof this.Bangumis[index][name] == "object") {
            this.Bangumis[index][name].push(newval);
          }
        }
      }
    },
    Remove: function (bid, name, orival) {
      for (let index = 0; index < this.Bangumis.length; index++) {
        if (this.Bangumis[index].ID == bid) {
          for (let i = 0; i < this.Bangumis[index][name].length; i++) {
            if (this.Bangumis[index][name][i] == orival) {
              this.Bangumis[index][name].splice(i, 1);
            }
          }
        }
      }
    },
    CheckDate: function (date) {
      var reg = /[0-9][0-9]-[0-1][0-9]-[0-3][0-9]/;
      if (reg.test(date) == true) {
        return true;
      } else {
        alert("!Wrong Date");
        return false;
      }
    },
    AddBangumi: function () {
      let id = prompt("Input ID of Bangumi Which Will Be Added");
      if (!id) {
        return;
      } else {
        this.Bangumis.push({
          ID: id,
          Name: "Name",
          Alias: ["Alias"],
          Type: "TV",
          Studios: ["Studio"],
          CoSubs: ["CoSubs"],
          TPSubs: ["TPSubs"],
          ReleaseDate: "20-20-20",
          Patches: ["Patch"],
          Set: "Set",
        });
      }
    },
    RemoveBangumi: function () {
      let id = prompt("Input ID of Bangumi Which Will Be Removed");
      if (!id) {
        return;
      } else {
        this.Bangumis = this.Bangumis.filter(function (x) {
          return x.ID != id;
        });
      }
    },
  },
};
</script>

<style>
.Bangumi + .Bangumi::before {
  content: "**********";
  display: block;
}

* {
  font-family: "Consolas", "Courier New", Courier, 'PingFang SC', 'Microsoft YaHei', monospace;
  margin: 0.1rem;
}
</style>