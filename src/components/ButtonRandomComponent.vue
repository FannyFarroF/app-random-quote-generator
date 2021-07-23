<template>
  <button class="btn d-flex align-items-center" @click="random()">
    random
    <span class="material-icons-outlined mx-2">
      autorenew
    </span>
  </button>
</template>

<script>
  export default {
    name: "ButtonComponent",
    created() {},
    props: {},
    data() {
      return {};
    },
    methods: {
      random() {
        this.$emit("random", true);
      },
    },
  };
</script>

<style lang="scss" scoped>
  button {
    border: 1px solid #eee !important;
    &:hover {
      background: #eee;
    }
  }
</style>
