<template>
  <div class="twitsdb">
    <h1>{{ msg }}</h1>
  </div>
</template>



<script>
export default {
  name: "TwittsDB",
  props: {
    msg: String
  }
};
</script>