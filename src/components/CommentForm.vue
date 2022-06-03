<template>
  <div>
    <div class="w-75 mx-auto">
      <h3>Add Comments</h3>
      <form @submit.prevent>
        <input
          v-model="comment.name"
          type="text"
          placeholder="name"
          class="form-control"
        />
        <input
          v-model="comment.email"
          type="text"
          placeholder="Email"
          class="form-control my-3"
        />
        <input
          v-model="comment.content"
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
export default {
  components: { MyButton },
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