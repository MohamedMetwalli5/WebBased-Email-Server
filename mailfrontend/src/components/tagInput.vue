<template>
  <div class="tag-input">
    <div v-for="(tag, index) in tags" :key="tag" class="tag-input__tag">
      <span @click="removeTag(index)">x</span>
      {{ tag }}
    </div>
    <input
      type="text"
      placeholder="Enter an email address:"
      class="tag-input__text"
      @keydown.enter="addTag"
      @keydown.down="addTag"
    />
  </div>
</template>
<script>
export default {
  name: "tagInput",
  data() {
    return {
      tags: [],
    };
  },
  methods: {
    addTag(event) {
      event.preventDefault();
      var val = event.target.value.trim();
      //if()
      if (val.length > 0) {
        this.tags.push(val);
        event.target.value = "";
      }
      this.$emit("addReceiver", this.tags);
    },
    removeTag(index) {
      this.tags.splice(index, 1);
      this.$emit("addReceiver", this.tags);
    },
  },
};
</script>
<style scoped>
.tag-input {
  width: 100%;
  border: 1px solid #eee;
  font-size: 0.9em;
  height: 50px;
  box-sizing: border-box;
  padding: 0 10px;
  border-radius: 5px;
}

.tag-input__tag {
  height: 30px;
  float: left;
  margin-right: 10px;
  background-color: #eee;
  margin-top: 10px;
  line-height: 30px;
  padding: 0 5px;
  border-radius: 5px;
}

.tag-input__tag > span {
  cursor: pointer;
  opacity: 0.75;
}

.tag-input__text {
  border: none;
  outline: none;
  font-size: 0.9em;
  line-height: 50px;
  background: none;
}
</style>