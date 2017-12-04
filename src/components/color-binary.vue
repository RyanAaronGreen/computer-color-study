<template>
  <div class="hello">

    <div class="color-wheel-container">
      <div class="color-wheel">
        <div class="color-wheel-color color-wheel--red" id="color-wheel--red">
        </div>
        <div class="color-wheel-color color-wheel--green" id="color-wheel--green">
        </div>
        <div class="color-wheel-color color-wheel--blue" id="color-wheel--blue">
        </div>
        <div class="color-wheel-color color-wheel--real" id="color-wheel--real">
        </div>
      </div>
    </div>

    <h1>{{ msg }}</h1>
    <p>{{ description }}</p>

    <div class="eightbit eightbit-r">
      <div class="bit">{{ red1 }}</div>
    </div>

    <div class="eightbit eightbit-r">
      <div class="bit">{{ red2 }}</div>
    </div>

    <div class="eightbit eightbit-g">
      <div class="bit">{{ green1 }}</div>
    </div>

    <div class="eightbit eightbit-g">
      <div class="bit">{{ green2 }}</div>
    </div>

    <div class="eightbit eightbit-b">
      <div class="bit">{{ blue1 }}</div>
    </div>

    <div class="eightbit eightbit-b">
      <div class="bit">{{ blue2 }}</div>
    </div>

    <input id="colorPicker" type="text" name="" placeholder="Type your hexcode here..." :onkeyup="convert()" v-model="hexcode">


  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Understanding Color',
      description: 'Every color is a combination of 24 bits (or 32 bits if the alpha channel is included).',
      hexcode: '',
      red1: '0000',
      red2: '0000',
      green1: '0000',
      green2: '0000',
      blue1: '0000',
      blue2: '0000',
      str: '',
      bytes: []
    }
  },

  mounted () {
    this.init()
  },

  computed: {
    convertToBinary: function (event) {
      // console.log(event)
      // console.log(this.hexcode)
      //
      // for (var i = 0; i < this.hexcode.length - 1; i += 2) {
      //   this.bytes.push(parseInt(this.hexcode.substr(i, 2), 16))
      // }
      // this.str = String.fromCharCode.apply(String, this.bytes)
    }
  },

  methods: {
    init () {
      this.setBinds()
      this.convert()
      this.setColorCircles()
    },

    setBinds () {
      this.redCircle = this.$el.querySelector('.color-wheel--red')
      this.greenCircle = this.$el.querySelector('.color-wheel--green')
      this.blueCircle = this.$el.querySelector('.color-wheel--blue')
      this.realCircle = this.$el.querySelector('.color-wheel--real')
    },

    setColorCircles (red, green, blue) {
      this.redCircle.style.backgroundColor = '#' + red + '0000'
      this.blueCircle.style.backgroundColor = '#00' + green + '00'
      this.greenCircle.style.backgroundColor = '#0000' + blue
      this.realCircle.style.backgroundColor = '#' + red + green + blue
    },

    convert () {
      if (this.hexcode.length === 6) {
        let hexValue = this.hexcode
        let hexArray = []

        for (let i = 0; i < hexValue.length; i++) {
          hexArray.push(parseInt(hexValue.substr(i, 1), 16).toString(2))

          switch (i) {
            case 0:
              this.red1 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
            case 1:
              this.red2 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
            case 2:
              this.green1 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
            case 3:
              this.green2 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
            case 4:
              this.blue1 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
            case 5:
              this.blue2 = parseInt(hexValue.substr(i, 1), 16).toString(2)
              break
          }
        }
        this.setColorCircles(hexValue.substr(0, 2), hexValue.substr(2, 2), hexValue.substr(4, 2))
        console.log(hexArray[0])
        console.log(hexArray[0].toString(10))
      }
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#colorPicker {
  background-color: transparent;
  border: 0;
  border-bottom: 2px solid #bbb;
  width: 300px;
  max-width: 100%;
  display: block;
  margin: 20px auto;
  font-size: 24px;
  text-align: center;
  transition: all 0.3s;
  color: #333;
}
#colorPicker:focus {
  outline: none;
  border-color: #888;
}

h1, h2 {
  font-weight: normal;
}

@keyframes rotateColorWheel {
  from {transform: rotate(0);}
  to {transform: rotate(360deg);}
}

.color-wheel-container {
  padding: 20px 0;
  display: block;
  width: 100%;
}
.color-wheel {
  animation-duration: 20s;
  animation-name: rotateColorWheel;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  display: inline-block;
  position: relative;
}
.color-wheel-color {
  transition: all 0.9s;
  height: 125px;
  width: 125px;
  background-size: 125px 125px;
  border-radius: 100%;
  display: inline-block;
  top: 50%;
  left: 50%;
}
#color-wheel--red {
  transform: translate(-60%, -60%);
  position: absolute;
  opacity: 1;
  mix-blend-mode: screen;
  background-color: #c0392b;
}
#color-wheel--green {
  transform: translate(-50%, -40%);
  position: absolute;
  opacity: 1;
  mix-blend-mode: screen;
  background-color: #2ecc71;
}
#color-wheel--blue {
  transform: translate(-40%, -60%);
  position: absolute;
  opacity: 1;
  mix-blend-mode: screen;
  background-color: #3498db;
}
#color-wheel--real {
  transform: translate(-50%, 0%);
  position: absolute;
  height: 75px;
  width: 75px;
  opacity: 1;
  z-index: 3;
  position: relative;
  background-color: #fff;
}
.eightbit {
  display: inline-block;
  margin: 0 2px;
}

.eightbit-r {
  border-bottom: 2px solid #ee0000;
}
.eightbit-g {
  border-bottom: 2px solid #00ee00;
}
.eightbit-b {
  border-bottom: 2px solid #0000ee;
}

.bit {
  display: inline-block;
  font-size: 4vw;
  border: 1px solid #dddddd;
  padding: 5px;
  background-color: #fefefe;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
