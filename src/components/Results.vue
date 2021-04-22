<template>
  <div class="results">
    <h1>Now that you have your results join the breakout room of the group you scored highest in.</h1>
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
          fill="#222"
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
    <div @click="test">clickme</div>
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
      bars: []
    }
  },
  methods: {
    test() {
      this.bars = [
        {
          "height": (this.resultsData.one / 100) * this.height,
          "x": 0,
          "y": this.height - ((this.resultsData.one / 100) * this.height)
        },
        {
          "height": (this.resultsData.two / 100) * this.height,
          "x": 133,
          "y": this.height - ((this.resultsData.two / 100) * this.height)
        },
        {
          "height": (this.resultsData.three / 100) * this.height,
          "x": 266,
          "y": this.height - ((this.resultsData.three / 100) * this.height)
        },
        {
          "height": (this.resultsData.four / 100) * this.height,
          "x": 399,
          "y": this.height - ((this.resultsData.four / 100) * this.height)
        }
      ]
    }
  }
}
</script>

<style>
  
</style>