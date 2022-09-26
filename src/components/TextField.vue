<script>
  export default {
    name: 'TextField',
    props: {
      content: {
        type: String,
        required: true
      }
    }
  }
</script>

<template>
  <textarea
    class="textfield"
    type="text"
    maxlength="500"
    v-model="content"
    @input="this.$emit('description', content)" />
</template>

<style scoped>
  .textfield {
    width: 100%;
    min-height: 2rem;

    padding-left: 0.4rem;

    background-color: rgb(203, 230, 255);
    border: 1px solid black;

    resize: vertical;
    transition: 0.2s;
  }

  .textfield:hover {
    background-color: rgb(184, 214, 241);
  }
  .textfield:focus {
    background-color: aliceblue;
    outline: none;
  }
</style>