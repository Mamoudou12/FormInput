<template>
  <div id="app">
    <UserForm />
  </div>
</template>

<script>
import UserForm from './components/UserForm.vue';

export default {
  name: 'App',
  components: {
    UserForm
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}
</style>
