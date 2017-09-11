<template>
  <body>
  <div class="hello">
    <div class="game">
      <div class="row">
        <div :class='{ selected : cubo1Selected, "cubo1 disabled":true}' id='cubo1' @click='addMove()'></div>
        <div class="cubo2 disabled" id='cubo2' @click='addMove()'></div>
      </div>
      <div class="row">
        <div class="cubo3 disabled" id='cubo3' @click='addMove()'></div>
        <div class="cubo4 disabled" id='cubo4' @click='addMove()'></div>
        <input type='text' id='objectiveInput' v-model='objective' placeholder="ingresa meta">
        <div class="btnStart" @click='startGame()'>Iniciar</div>
        <h2>Moves</h2>
        <ul>
          <li v-for='move in moves'>{{move}}</li>
        </ul>
        <h2>Sequence</h2>
        <ul>
          <li v-for='element in sequence'>{{element}}</li>
        </ul>
        <h1>{{objective}}</h1>
        <button @click='createSequence()'>crear secuencia</button>
        <div @click='paintCube()' >Pintar Bloque</div>
      </div>
    </div>
  </div>
</body>
</template>

<style>
.cubo1{
  background-color: #9f4848;
  width: 4rem;
  height: 4rem
}
.cubo2{
  background-color: #3e3e7e;
  width: 4rem;
  height: 4rem
}
.cubo3{
  background-color: #305530;
  width: 4rem;
  height: 4rem
}
.cubo4{
  background-color: #7a7a20;
  width: 4rem;
  height: 4rem
}
.row{
  display: flex;
}
.btnStart{
  background-color: gray;
  height:2rem
}
.disabled{
  background-color: gray;
}
.selected{
  background-color: orange;
  width: 6rem;
  height: 6rem;
}
</style>

<script>

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      moves: [],
      objective: 0,
      sequence: [],
      level: 1,
      highlighted: '',
      cubo1Selected: false,
      claseCubo1: ''
    }
  },
  methods: {
    addMove: function () {
      if (!event.path[0].classList.value.includes('disabled')) {
        this.moves.push(event.srcElement.id)
      }
    },
    startGame: function () {
      // if (this.objective > 0) {
      document.getElementById('objectiveInput').disabled = true
      Array.from(document.getElementsByClassName('disabled')).forEach(function (element) {
        element.classList.remove('disabled')
      })
      // } else {
      // alert('meta debe ser mayor a 1')
      // }
    },
    paintCube: function () {
      console.log('paintedCube')
      // this.cubo1Selected = true

      this.claseCubo1 = 'selected'

      this.cubo1Selected = true
      sleep(1000)
      this.cubo1Selected = false
    },
    unpaintCube: function (cubeId) {
      document.getElementById(cubeId).classList.remove('selected')
    },
    createSequence: function () {
      var arr = 'cubo' + Math.floor(Math.random() * 4 + 1)
      this.sequence.push(arr)
      this.level++
      // console.log('level ' + this.level)
      // console.log('sequence ' + this.sequence.toString())
      this.sequence.forEach((anElement) => {
        sleep(1000)
        console.log(anElement)
        sleep(1000)
        this.paintCube(anElement)
        this.unpaintCube(anElement)
      })
    }
  }
}
function sleep (milliseconds) {
  var start = new Date().getTime()
  for (var i = 0; i < 1e7; i++) {
    if ((new Date().getTime() - start) > milliseconds) {
      break
    }
  }
}

</script>
