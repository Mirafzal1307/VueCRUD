<template>
  <div class="comment">
    <div>
      <p>
        {{ comment.name }} <b> {{ comment.email }} </b>
      </p>
      <b> Content:{{ comment.content }} </b>
    </div>
    <div>
      <my-button class="btn btn-danger"> Delete </my-button>
    </div>
  </div>
</template>

<script>
export default {

  props: {
    comment: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped >
.comment {
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
