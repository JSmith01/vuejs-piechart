<template>
  <div>
    <PieChart :data="data" :diameter="120" />
    <div>
      <button @click="generate">Generate new data</button>
    </div>
  </div>
</template>

<script>
import PieChart from './PieChart';

export default {
  name: 'app',

  components: { PieChart },

  mounted() {
    this.generate();
  },

  data() {
    return { data: [] }
  },

  methods: {
    generate() {
      this.data = Array.from({ length: Math.floor(Math.random() * 6 + 2) }, () => Math.floor(Math.random() * 100 + 1));
    }
  }
}
</script>
