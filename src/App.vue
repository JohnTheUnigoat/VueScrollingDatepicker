<template>
  <div id="app">
    <img src="./assets/logo.png">

    <scrolling-datepicker />
  </div>
</template>

<script>
import ScrollingDatepicker from './components/ScrollingDatepicker.vue';

export default {
  name: 'App',
  components: {
    ScrollingDatepicker,
  }
}
</script>

