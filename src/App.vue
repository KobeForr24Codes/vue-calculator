<template>
  <v-app>
    <v-card class="mx-auto my-auto" width="500">
      <div style="background-color: #1C1C1C" class="text-end pa-5">
        <v-sheet color="#1C1C1C" class="pa-5 display-3 white--text" tile>{{ displayInputs || 0 }}</v-sheet>
      </div>
      <v-row no-gutters>
        <v-col
          v-for="item in majorLine"
          :key="item.index"
          cols="12"
          sm="3"
          class="border-color"
        >
          <v-sheet
            tile
            v-ripple
            :color="item.color"
            class="pa-5 text-center display-3 calc-btn"
            @click="onPress(item.sign)"
          ><span :class="item.textColor">{{ item.sign }}</span></v-sheet>
        </v-col>
        <v-col
          cols="12"
          sm="6"
          class="border-color"
        >
          <v-sheet
            tile
            v-ripple
            color="#EEEEEE"
            class="pa-5 text-center display-3 calc-btn"
            @click="onPress('0')"
          >0</v-sheet>
        </v-col>
        <v-col
          cols="12"
          sm="3"
          class="border-color"
        >
          <v-sheet
            tile
            v-ripple
            color="#EEEEEE"
            class="pa-5 text-center display-3 calc-btn"
            @click="onPress('.')"
          >.</v-sheet>
        </v-col>
        <v-col
          cols="12"
          sm="3"
          class="border-color"
        >
          <v-sheet
            tile
            v-ripple
            color="#FF9500"
            class="pa-5 text-center display-3 calc-btn white--text"
            @click="onEquals"
          >=</v-sheet>
        </v-col>
        <!-- <v-col
          v-for="item in bottomLine"
          :key="item.index"
          cols="12"
          sm="3"
          class="border-color"
        >
          <v-sheet
            tile
            v-ripple
            :color="item.color"
            class="pa-5 text-center display-3 calc-btn"
            @click="onPress(item.sign)"
          ><span :class="item.textColor">{{ item.sign }}</span></v-sheet>
        </v-col> -->
      </v-row>
    </v-card> 
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data () {
    return {
      majorLine: [
        {sign: 'C', color: '#D4D4D2'},
        {sign: '±', color: '#D4D4D2'},
        {sign: '%', color: '#D4D4D2'},
        {sign: '÷', color: '#FF9500', textColor: 'white--text'},
        {sign: 7, color: '#EEEEEE'},
        {sign: 8, color: '#EEEEEE'},
        {sign: 9, color: '#EEEEEE'},
        {sign: '×', color: '#FF9500', textColor: 'white--text'},
        {sign: 4, color: '#EEEEEE'},
        {sign: 5, color: '#EEEEEE'},
        {sign: 6, color: '#EEEEEE'},
        {sign: '-', color: '#FF9500', textColor: 'white--text'},
        {sign: 1, color: '#EEEEEE'},
        {sign: 2, color: '#EEEEEE'},
        {sign: 3, color: '#EEEEEE'},
        {sign: '+', color: '#FF9500', textColor: 'white--text'}
      ],
      bottomLine: [
        {sign: '.', color: '#EEEEEE'},
        {sign: '=', color: '#FF9500', textColor: 'white--text'}
      ],
      displayInputs: '',
      inputs: '',
      calculation: [],
      operatorsToChange: ['×', '÷'],
      operators: ['+', '-', '÷', '×']
    }
  },
  methods: {
    onPress (sign) {
      this.displayInputs += sign
      if (sign === 'C') this.displayInputs = this.inputs = ''
      if (this.operatorsToChange.includes(sign)) {
        if (sign === '×' ) {
          this.inputs += '*'
        } else {
          this.inputs += '/'
        }
      } else {
        this.inputs += sign
      }
    },
    onEquals () {
      let str = '' + this.inputs
      if (str.slice(-1) === '%') {
        str.slice(0, -1)
        this.getPercentage(str)
      } else {
        this.displayInputs = this.inputs = eval(this.displayInputs)
      }
    },
    getPercentage (input) {
      this.displayInputs = this.inputs = parseInt(input) / 100
    }
  }
}
</script>

<style scoped>
  .border-color {
    border: 1.2px solid #505050;
  }
  .calc-btn {
    cursor: pointer;
  }
</style>
