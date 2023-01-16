<template>
  <BewilligungsList :antraege="data" :changeBewilligung="changeBewilligung" />
</template>

<script>
import BewilligungsList from './BewilligungsList.vue';
import data from '../../public/antraege.json';

export default {
  components: { BewilligungsList },
  setup() {
    function changeBewilligung(antrag) {
      data[antrag].bewilligt = !data[antrag].bewilligt;
      console.log(antrag + ' bewilligt: ' + data[antrag].bewilligt);
    }

    return { data, changeBewilligung };
  },
};
</script>

<style scoped></style>
