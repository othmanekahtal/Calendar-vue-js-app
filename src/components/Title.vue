<template>
  <h1>{{ text }}</h1>
</template>

<script>

export default {
  name: "Title",
  props: {
    text: {
      type: String,
      default: 'H1 Title here'
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  margin-bottom: 2.5rem;
  text-transform: capitalize;
  font-size: 3.75rem;
  font-weight: 800;
  transition: 0.45s ease-in-out;
  &:hover {
    transform: skewY(2deg) skewX(3.5deg) scale(1.5);
    text-shadow: 0.5rem 1rem 1.5rem rgba(#000000, 0.2);
  }
}
</style>