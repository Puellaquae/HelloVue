<template>
  <input
    onchange="this.blur()"
    v-on:keypress.enter="change"
    :style="{width: textwitdh}"
    type="text"
    v-model="Value"
  />
</template>

<script>
export default {
    name: 'auto-input',
    props: ['val', 'check'],
    data: function () {
        return {
            OriValue: this.val,
            Value: this.val
        }
    },
    computed: {
        textwitdh: function () {
            return this.Value.length + 'ch';
        }
    },
    methods: {
        change: function () {
            if (this.Value != this.OriValue) {
                if (this.check != null && this.check != undefined && typeof this.check == 'function') {
                    if (this.check(this.Value) == true) {
                        this.$emit('submit', this.OriValue, this.Value);
                        this.OriValue = this.Value;
                    } else {
                        this.Value = this.OriValue;
                    }
                } else {
                    this.$emit('submit', this.OriValue, this.Value);
                    this.OriValue = this.Value;
                }
            }
        }
    }
}
</script>

<style scoped>
* {
    border: none;
    font-size: 1rem;
}
</style>