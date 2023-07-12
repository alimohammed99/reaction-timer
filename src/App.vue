
<template>
    <h1>
        <marquee behaviour="slide" direction="left" scrollamount="20" style="font-size:35px; color:tomato; border:25px double black; border-radius:20px">NINJA REACTION TIME</marquee>
    </h1>
    
    <h3 v-if="isPlaying" style="color:rgb(80, 224, 80); background:black; border-radius:20px; font-size:25px; padding:15px">Click the green box quickly when it appears, let's test your speed.</h3>
    
    <button v-if="!isPlaying" title="Click to start new game" id="play" @click="startGame">PLAY</button>
    <button disabled v-if="isPlaying" title="Game is ON already" id="play2" @click="startGame">PLAY</button>
    <!-- I have 2 buttons because I want the Play button to have different stylings when game is ON and when game is not ON. -->
    
    <Block v-if="isPlaying" :delay="delay" @end="endGame" />
    
    <Results v-if="showResult" :score="score" />
    
    <div style="text-align: left;">
        <h3>RANKING LEVELS:</h3>
        <ul style="font-size:20px;">
            <li>NINJA FINGERS ~ <span style="font-style:italic; color:white; background:green; padding:3px">Best</span></li>
            <li>RAPID FLEXES ~ <span style="font-style:italic; color:white; background:blue; padding:3px">Average</span></li>
            <li>SNAIL PACE ~ <span style="font-style:italic; color:white; background:red; padding:3px">Low</span></li>
        </ul>
    </div>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
export default {
    name: 'App',
    components: { Block, Results },
    data() {
        return {
            isPlaying: false,
            delay: null,
            score: null,
            // for final result
            showResult: null
        }
    },
    methods: {
        startGame() {
            this.delay = 2000 + Math.random() * 5000
            this.isPlaying = true
            this.showResult = false
        },
        endGame(reactionTime) {
            // Because when I emitted in Block.vue, I passed along a data(this.reactionTime). That's why it's added as an argument and definitely, a new var can be used to store it.
            this.score = reactionTime
            this.isPlaying = false
            this.showResult = true
        }
    }
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 30px;
}

#play {
    padding: 25px;
    border-radius: 20px;
    color: white;
    background: rgb(223, 15, 84);
    font-size: 25px;
    cursor: pointer;
    box-shadow: 9px 9px 8px yellow;
    letter-spacing: 1px;
}

#play2 {
    padding: 25px;
    border-radius: 20px;
    font-size: 25px;
    cursor: not-allowed;
    opacity: 0.7;
}

body {
    background: repeating-radial-gradient(lightblue, white 10%, lightgreen 15%);
    border: 20px dotted black;
    padding: 90px;
}
</style>