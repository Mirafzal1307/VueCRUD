<template>
<navbar class="container" :showModal="showModal" />
  <div>
    <my-modal  v-model:show="modalVisible" >
    <comment-form @addComment="createComments" />
    </my-modal>
    <comment-list :comments="comments" @remove="removeComment" />
  </div>
</template>

<script>
import CommentForm from "./components/CommentForm";
import CommentList from "./components/CommentList";
import Navbar from "@/components/Navbar"


export default {
  components: {
    CommentForm,
    CommentList,
    Navbar

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
      modalVisible: false
    };
  },
  methods: {
    createComments(comment) {
      this.comments.push(comment);
    },
    removeComment(comment){
          this.comments = this.comments.filter(c => c.id !== comment.id);
    },
    showModal(){
      this.modalVisible = true;
    }
  },
};
</script>

<style>
</style>

<!-- </style> -->