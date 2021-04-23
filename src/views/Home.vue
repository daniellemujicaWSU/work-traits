<template>
  <div class="home">
    <WorkStyleInventory @quizResults="showResults($event)" v-if="!quizComplete"/>
    <Results :resultsData="results" v-if="quizComplete"/>
  </div>
</template>

<script>
// @ is an alias to /src
import WorkStyleInventory from '@/components/WorkStyleInventory.vue'
import Results from '@/components/Results.vue'
import workTraitScoringMap from '../work-trait-scoring-map.json'

export default {
  name: 'Home',
  components: {
    WorkStyleInventory,
    Results
  },
  data() {
    return {
      results: {
        "one": 80,
        "two": 30,
        "three": 20,
        "four": 15
      },
      quizComplete: false
    }
  },
  methods: {
    showResults(results) {
      this.quizComplete = true
      this.results.one = workTraitScoringMap.One[results.one]
      this.results.two = workTraitScoringMap.Two[results.two]
      this.results.three = workTraitScoringMap.Three[results.three]
      this.results.four = workTraitScoringMap.Four[results.four]
    },
    test() {
      console.log(workTraitScoringMap.One[this.results.one], this.results.one)
    }
  }
}
</script>
