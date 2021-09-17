<template>
  <div class="multi-input">
    <div class="valueBox" v-if="workingValue.length > 0">
      <span
        class="item"
        v-for="(item, index) in workingValue"
        :key="index"
        @click.self="editVal(index)"
      >
        <span class="remove" @click.stop="workingValue.splice(index, 1)">
          ×
        </span>
        {{ item }}
      </span>
    </div>
    <input type="text" @keyup="keyPress" ref="input" />
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Array,
      default() {
        return [];
      },
    },
    split: {
      type: Array,
      default() {
        return [","];
      },
    },
  },
  emits: ["update:modelValue"],
  data() {
    return {
      workingValue: this.modelValue,
    };
  },
  methods: {
    editVal(index) {
      this.$refs.input.value = this.workingValue.splice(index, 1)[0];
    },
    keyPress(e) {
      let value = e.target.value;
      if (e.key == "Enter" || this.split.includes(e.key)) {
        if (this.split.includes(e.key)) {
          value = value.slice(0, -1);
        }
        this.workingValue.push(value);
        e.target.value = "";
      } else if (
        e.keyCode === 8 &&
        e.target.value == "" &&
        this.workingValue.length > 0
      ) {
        e.target.value = this.workingValue.pop();
      }
    },
  },
  watch: {
    workingValue: {
      handler(n) {
        this.$emit("update:modelValue", n);
      },
      deep: true,
    },
  },
};
</script>

<style>
.multi-input {
  border-style: solid;
  border-width: 2px;
  border-radius: 3px;
  display: inline-block;
  border-color: #666;
  min-width: 300px;
  max-width: 100%;
}

.multi-input input {
  border: none;
  padding: 5px;
  background-color: rgba(0, 0, 0, 0);
  width: 100%;
  /* border-color: #eee; */
}
.multi-input input:focus {
  border: none;
  outline: none;
}

.multi-input .valueBox {
  padding: 5px;
}

.multi-input .valueBox .item {
  padding: 3px 5px;
  margin: 2px;
  display: inline-block;
  background-color: #eee;
  border-radius: 10px;
  cursor: text;
}

.multi-input .valueBox .item .remove {
  padding: 2px;
  display: inline-block;
  width: 18px;
  text-align: center;
  color: white;
  cursor: pointer;
  /* height: 10px; */
  background-color: #bb1111;
  border-radius: 100px;
}
</style>
