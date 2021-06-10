<template>
  <calender/>
</template>
<script>
import Calender from './components/Calender';
import "./assets/style.scss";

export default {
  name: 'App',
  components: {
    Calender
  },
  methods: {

  },
  data(){
    return {

    }
  },
  computed:{

  }
}
</script>

<style lang="scss">
#app {
  padding: 2.5rem (2.5rem +2.5rem / 2 );
  font-family: 'Karla', sans-serif;
  text-align: center;
  color: #444;
  background-color: #f5f5f5;
  border-radius: 1rem;
  box-shadow: 0 0 5.5rem rgba(#444,.5);
  transition: .25s linear;
}
</style>
