<template>
  <div>
    <comment-form @addComment="createComments" />
    <comment-list v-bind:comments="comments" />
  </div>
</template>

<script>
import CommentForm from "./components/CommentForm";

import CommentList from "./components/CommentList";

export default {
  components: {
    CommentForm,
    CommentList,
  },
  data() {
    return {
      comments: [
        {
          id: 1,
          name: "Samar mirafzal",
          email: "usmonjonovmirafzal0713@gmail.com ",
          content: "dddddd  ddd dd ",
        },
        {
          id: 2,
          name: "Jasur mirafzal",
          email: "Nemar@gmail.com ",
          content: "dddddd dd dd  ddd dd ",
        },
        {
          id: 3,
          name: "Nemar mirafzal",
          email: "Samr@gmail.com ",
          content: "dddddd  drer ddd dd ",
        },
      ],
    };
  },
  methods: {
    createComments(comment) {
      this.comments.push(comment);
    },
  },
};
</script>

<style>
</style>

<!-- </style> -->