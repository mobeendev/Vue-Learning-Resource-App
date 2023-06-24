<template>
  <base-card>
    <div>add resources...</div>

    <form @submit.prevent="saveForm">
      <input type="text" placeholder="enter title" ref="title" />
      <br />
      <textarea rows="10" ref="description">Enter Description</textarea>
      <br />
      <input type="text" placeholder="enter link" ref="link" />
      <br />
      <base-button type="submit"> Add New Resource </base-button>
    </form>
  </base-card>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';
export default {
  inject: ['myMethod'],

  components: { BaseButton },
  setup() {},
  data() {
    return {};
  },
  methods: {
    saveForm: function () {
      let title = this.$refs.title.value;
      let description = this.$refs.description.value;
      let link = this.$refs.link.value;
      this.myMethod(title, description, link);
      console.log(title, description, link);
    },
  },
};
</script>
