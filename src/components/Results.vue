<template>
  <div class="results">
    <h1>Now that you have your results join the breakout room of the group you scored highest in.</h1>
    <div class="bar-chart-container">
      <svg 
        class="barchart" 
        :width="width" 
        :height="height">
        <g 
          class="bars" 
          fill="none">
          <g 
            fill="none" 
            v-for="(bar, index) in bars" 
            :key="index">
          <rect
            fill="#4F868E"
            :height="bar.height"
            width="100"
            :x="bar.x"
            :y="bar.y">
            <animate 
              attributeType="CSS" 
              attributeName="height" 
              :from="0"
              :to="bar.height"
              dur="1s"/>
          </rect>
          <text 
            :x="bar.x + 20" 
            :y="bar.y + bar.height - 20" 
            fill="white">Group {{ index + 1 }}
          </text>
          </g>
        </g>
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'resultsData'
  ],
  data() {
    return {
      height: 400,
      width: 500,
      bars : [
        {
          "height": (this.resultsData.one / 100) * 400,
          "x": 0,
          "y": 400 - ((this.resultsData.one / 100) * 400)
        },
        {
          "height": (this.resultsData.two / 100) * 400,
          "x": 133,
          "y": 400 - ((this.resultsData.two / 100) * 400)
        },
        {
          "height": (this.resultsData.three / 100) * 400,
          "x": 266,
          "y": 400 - ((this.resultsData.three / 100) * 400)
        },
        {
          "height": (this.resultsData.four / 100) * 400,
          "x": 399,
          "y": 400 - ((this.resultsData.four / 100) * 400)
        }
      ]
    }
  }
}
</script>

<style>
  .bar-chart-container {
    text-align: center;
  }
  .barchart {
    border-bottom: 3px solid black;
  }
</style>