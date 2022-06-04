<template>
  <div>
    <div class="w-75 mx-auto">
      <h3>Add Comments</h3>
      <form @submit.prevent>
        <my-input
          v-model:modelValue="comment.name"
          type="text"
          placeholder="name"
          class="form-control"
        />
        <my-input
          v-model:modelValue="comment.email"
          type="text"
          placeholder="Email"
          class="form-control my-3"
        />
        <my-input
          v-model:modelValue="comment.content"
          type="text"
          placeholder="Content"
          class="form-control"
        />
        <div class="d-flex flex-row-reverse">
          <my-button class="btn btn-primary mt-3" @click="createComment">
            Add Comments
          </my-button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import MyButton from './UI/MyButton.vue';
import MyInput from './UI/MyInput.vue';
export default {
  components: { MyButton, MyInput },
  data() {
    return {
      comment: {
        name: "",
        email: "",
        content: "",
      },
    };
  },
  methods: {
    createComment() {
      this.comment.id = Date.now();
      this.$emit("addComment", this.comment);
      this.comment = {
        name: "",
        email: "",
        content: "",
      };
    },
  },
};
</script>

<style>
</style>