<template>
  <div>
    <h1>Work Styles Inventory</h1>
    <h2>Select the word or phrase in each set that is most like you. You must choose one from each group in order to get your results.</h2>
    <div class="quizWrapper">
      <!-- <div v-for="(traits, key, index) in traitSet" :key="key">
        <h3>Set {{ index + 1 }}</h3>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[index]" :value="traits.one.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ traits.one.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[index]" :value="traits.two.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ traits.two.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[index]" :value="traits.three.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ traits.three.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[index]" :value="traits.four.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ traits.four.trait }}</span>
        </label>
      </div> -->
      <div>
        <h3>Set {{ currentSet + 1 }}</h3>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[currentSet]" :value="Object.values(traitSet)[currentSet].one.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ Object.values(traitSet)[currentSet].one.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[currentSet]" :value="Object.values(traitSet)[currentSet].two.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ Object.values(traitSet)[currentSet].two.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[currentSet]" :value="Object.values(traitSet)[currentSet].three.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ Object.values(traitSet)[currentSet].three.trait }}</span>
        </label>
        <label class="radio">
          <span class="radio__input">
            <input type="radio" v-model="setValues[currentSet]" :value="Object.values(traitSet)[currentSet].four.value" />
            <span class="radio__control"></span>
          </span>
          <span class="radio__label">{{ Object.values(traitSet)[currentSet].four.trait }}</span>
        </label>
      </div>
      <div class="button-container">
        <div :class="[currentSet === 0 ? 'disable' : '', complete ? 'hide' : '', 'button', 'prev']" @click="prevSet">Previous</div>
        <div :class="[currentSet === 23 ? 'disable' : '', complete ? 'hide' : '', 'button', 'next']" @click="nextSet">Next</div>
        <div :class="[complete ? '' : 'hide', 'button', 'submit']" @click="submitAnswers">Submit</div>
      </div>
    </div>
    
  </div>
</template>

<script>
import traitBank from '../work-trait-bank.json'
export default {
  data() {
    return {
      traitSet: traitBank,
      currentSet: 0,
      setValues: {
        setOne: null,
        setTwo: null,
        setThree: null,
        setFour: null,
        setFive: null,
        setSix: null,
        setSeven: null,
        setEight: null,
        setNine: null,
        setTen: null,
        setEleven: null,
        setTwelve: null,
        setThirteen: null,
        setFourteen: null,
        setFifteen: null,
        setSixteen: null,
        setSeventeen: null,
        setEighteen: null,
        setNineteen: null,
        setTwenty: null,
        setTwentyOne: null,
        setTwentyTwo: null,
        setTwentyThree: null,
        setTwentyFour: null
      },
      score: {
        one: 0,
        two: 0,
        three: 0,
        four: 0
      }
    }
  },
  computed: {
    complete() {
      return Object.values(this.setValues).filter(value => value !== null).length === 24 ? true : false
    }
  },
  methods: {
    submitAnswers() {
      this.score.one = Object.values(this.setValues).filter(value => value === 1).length
      this.score.two = Object.values(this.setValues).filter(value => value === 2).length
      this.score.three = Object.values(this.setValues).filter(value => value === 3).length
      this.score.four = Object.values(this.setValues).filter(value => value === 4).length

      this.$emit('quizResults', this.score)
    },
    nextSet() {
      console.log('clicked', this.currentSet)
      if(this.currentSet < 23) {
        this.currentSet++
      }
    },
    prevSet() {
      if(this.currentSet > 0) {
        this.currentSet--
      }
    }
  }
}
</script>

<style>

  .quizWrapper {
    border: solid 3px #222222;
    border-radius: .25rem;
    padding: 2rem;
  }

  *,
  *:before,
  *:after {
    box-sizing: border-box;
  }

  .radio {
    font-size: 1.25rem;
    color: #4F868E;
    display: grid;
    grid-template-columns: min-content auto;
    grid-gap: 0.5em;
    margin-bottom: 1rem;
    padding: 1rem .5rem;
    border: solid 3px #4F868E;
    border-radius: .25rem;
  }
  
  .radio__input input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .radio__control {
    display: block;
    width: 1em;
    height: 1em;
    border-radius: 50%;
    border: 0.1em solid currentColor;
    transform: translateY(-0.05em);
  }

  .radio__input {
    display: flex;
  }

  .radio__label {
    line-height: 1;
  }

  input:checked + .radio__control {
    background: radial-gradient(#4F868E 50%, rgba(255, 0, 0, 0) 51%);
  }

  .button {
    padding: 1rem 0;
    width: 10rem;
    border-radius: .25rem;
    text-align: center;
    background: #4F868E;
    color: white;
    font-weight: bold;
    transition: background 300ms ease;
    cursor: pointer;
    margin-top: 1rem;
  }

  .button:hover {
    background: #3e6a71;
  }

  .disable {
    pointer-events: none;
    background: grey;
  }

  .hide {
    display: none;
  }

  .button-container {
    display: flex;
  }

  .next {
    margin-left: auto;
  }
  
</style>