<template>
  <svg class="pie">
    <circle
        v-for="item in dataObjects"
        v-bind:style="{strokeDasharray: `${item.relativeSize} ${circleLength}`, strokeDashoffset: -item.offset}"
        r="25%"
        cx="50%"
        cy="50%"
    />
  </svg>
</template>

<script>
  export default {
    name: 'PieChart',

    props: {
      data: { type: Array, required: true },
      diameter: { type: Number, required: true }
    },

    computed: {
      circleLength() {
        return this.diameter * Math.PI;
      },

      dataObjects() {
        let offset = 0;
        let total = this.data.reduce((c, i) => c + i, 0) || 1;

        return this.data.map(item => {
          let relativeSize = ((item / total) * this.circleLength);

          let dataObject = { relativeSize, offset };

          offset += relativeSize;

          return dataObject;
        })
      }
    }
  }
</script>

<style lang="scss">
  .pie circle {
    fill: none;
    stroke-width: 32;
    transition: stroke-dasharray 0.3s ease-in-out, stroke-dashoffset 0.3s ease-in-out;
  }

  $colors: red, yellow, cyan, blue, green, black, gray, purple;

  @for $i from 1 through length($colors) {
    .pie circle:nth-child(#{$i}) {
      stroke: nth($colors, $i);
    }
  }
</style>
