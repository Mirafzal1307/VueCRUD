<template>
  <navbar class="container" :showModal="showModal" />

  <div>
    <my-modal v-model:show="modalVisible">
      <comment-form @addComment="createComments" />
    </my-modal>
    <comment-list
      :comments="comments"
      @remove="removeComment"
      v-if="!isLoading"
    />
    <div v-else class="d-flex justify-content-center">
      <div class="spinner-grow" role="status">
        <span class="visually-hidden"> Loading...</span>
      </div>
    </div>
  </div>
</template>

<script>
import CommentForm from "./components/CommentForm";
import CommentList from "./components/CommentList";
import Navbar from "@/components/Navbar";
import axios from "axios";

export default {
  components: {
    CommentForm,
    CommentList,
    Navbar,
  },
  data() {
    return {
      comments: [],
      modalVisible: false,
      isLoading: false,
     
    };
  },
  methods: {
    createComments(comment) {
      this.comments.push(comment);
    },
    removeComment(comment) {
      this.comments = this.comments.filter((c) => c.id !== comment.id);
    },
    showModal() {
      this.modalVisible = true;
    },
    async fetchComments() {
      try {
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/comments?_limit=10"
        );
        this.comments = response.data;
        this.isLoading = false;
      } catch (e) {
        alert("Something went wrong");
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.fetchComments();
  },
};
</script>

<style>
</style>

<!-- </style> -->