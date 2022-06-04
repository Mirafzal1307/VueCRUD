<template>
  <div v-show="comments.length > 0">
    <h3 class="text-center text-primary" >Comments</h3>
    <comment-item
      class="w-75 mx-auto comment"
      v-for="comment in comments"
      :comment="comment"
      :key="comment.id"
      @remove="$emit('remove', comment)"
    />
  </div>
  <div v-show="comments.length === 0">
    <h2 class="text-center text-danger" >We can not found any comments yet </h2>
  </div>

  <div></div>
</template>

<script>
import CommentItem from "./CommentItem";
export default {
  components: {
    CommentItem,
  },
  props: {
    comments: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.comment {
  border: 5px solid #ccc;
  padding: 10px;
  margin: 10px;
}
</style>