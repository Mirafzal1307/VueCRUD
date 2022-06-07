<template>
  <div class="comment">
    <div>
      <p>
        {{ comment.name }}
      </p>
      <b> Content: </b>{{ comment.body }} <br />
      <b> {{ comment.email }} </b>
    </div>
    <div class="d-flex" >
      <my-button class="btn btn-secondary " @click="$router.push(`/comment/${comment.id} `)">
        Open
      </my-button>

      <my-button class="btn btn-danger" @click="$emit('remove', comment)">
        Delete
      </my-button>
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
