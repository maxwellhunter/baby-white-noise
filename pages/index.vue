<template>
  <div class="container" :style="determineStyle">
    <div v-for="noiseType in noiseTypes" @click="setNoiseType(noiseType)" class="color-selection-item">
      {{noiseType}}
    </div>
    <button @click="pressButton()">
      {{!this.playing ? 'play' : 'pause'}}
    </button>
  </div>
</template>

<script>
  import Tone from 'tone'

  export default {
    data () {
      return {
        playButtonText: 'Play',
        playing: false,
        selectedNoiseType: 'pink',
        noiseTypes: ['pink', 'brown', 'white']
      }
    },
    computed:{
      determineStyle(){
        let backgroundColor= ''
        if (this.selectedNoiseType === 'pink') { backgroundColor = '#E9C1CD'}
        if (this.selectedNoiseType === 'brown') { backgroundColor = '#443846'}
        if (this.selectedNoiseType === 'white') {backgroundColor = 'white'}
        return `background-color: ${backgroundColor}`
      }
    },
    methods: {
      pressButton () {
        if (this.playing) {
          this.stop()
        } else {
          this.start()
        }
      },
      setNoiseType(noiseType){
        this.selectedNoiseType = noiseType;
        if(this.playing){
          this.stop()
        }

      },
      start () {
        this.playing = true
        this.noise = new Tone.Noise(this.selectedNoiseType)
        this.noise.start().toMaster()
      },
      stop () {
        this.noise.stop()
        this.playing = false
      }
    }
  }
</script>

<style>
  .color-selection-item{
    cursor:pointer;
  }
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    flex-direction: column;
    transition: 1s ease-in-out;
  }

  .title {
    font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }
</style>
