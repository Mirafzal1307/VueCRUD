<template>
  <div>
    <comment-item
      class="w-75 mx-auto comment"
      v-for="comment in comments"
      :comment="comment"
      :key="comment.id"
    >
    </comment-item>
  </div>
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