<template>
  <navbar class="container" :showModal="showModal" />

  <div>
    <my-modal v-model:show="modalVisible">
      <comment-form @addComment="createComments" />
    </my-modal>
    <div class="d-flex container">
      <my-input
        v-model="searchQuery"
        class="form-control"
        placeholder="Search..."
      />
      <my-select
        class="w-25 m-auto"
        v-model="selectedSort"
        :options="selectOptions"
      />
      <my-button
        @click="showModal"
        class="mt-2 py-2 btn btn-primary text-decoration-none"
        href="#"
      >
        Add
      </my-button>
    </div>

    <comment-list
      :comments="sortAndSearchComments"
      @remove="removeComment"
      v-if="!isLoading"
    />
    <div v-else class="d-flex justify-content-center">
      <div class="spinner-grow" role="status">
        <span class="visually-hidden"> Loading...</span>
      </div>
    </div>
    <div class="page_wrapper container">
      <div
        class="btn btn-primary mx-1"
        :class="{ 'current-page': page === pageNum }"
        @click="changePage"
        v-for="pageNum in totalPage"
        :key="pageNum.id"
      >
        {{ pageNum }}
      </div>
    </div>
  </div>
</template>

<script>
import CommentForm from "@/components/CommentForm";
import CommentList from "@/components/CommentList";
import axios from "axios";

export default {
  components: {
    CommentForm,
    CommentList,
 
  },
  data() {
    return {
      comments: [],
      modalVisible: false,
      isLoading: false,
      selectedSort: "",
      searchQuery: "",
      page: 1,
      limit: 50,
      totalPage: 0,
      selectOptions: [
        { value: "name", name: "Filter by name" },
        { value: "email", name: "Filter by email" },
      ],
    };
  },
  methods: {
    createComments(comment) {
      this.comments.push(comment);
      this.modalVisable = false;
    },
    removeComment(comment) {
      this.comments = this.comments.filter((c) => c.id !== comment.id);
    },
    showModal() {
      this.modalVisible = true;
    },
    changePage() {
      this.page = this.page + 1;
      this.fetchComments();
    },
    async fetchComments() {
      try {
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/comments",
          {
            params: {
              _limit: this.limit,
              _page: this.page,
            },
          }
        );
        this.totalPage = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.comments = response.data;
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
  computed: {
    filteredComments() {
      return [...this.comments].sort((a, b) => {
        if (this.selectedSort === "name") {
          return a.name.localeCompare(b.name);
        } else if (this.selectedSort === "email") {
          return a.email.localeCompare(b.email);
        }
      });
    },
    sortAndSearchComments() {
      return this.filteredComments.filter((comment) => {
        return (
          comment.name.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          comment.email.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      });
    },
  },
  watch: {},
};
</script>

<style>
.current-page {
  background-color: #fff;
  color: #000;
}
</style>

<!-- </style> -->