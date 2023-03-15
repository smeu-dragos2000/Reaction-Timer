<template>
    
        <div class="target-container"
            v-if="showTarget"
            v-bind:style="{left: positionX + '%', top: positionY + '%'}"
        >
            <TargetCircle :class="{white: true}" :precision="20"  @created="stopTimer"/>
            <TargetCircle :class="{black: true}"  :precision="40" @created="stopTimer"/>
            <TargetCircle :class="{blue: true}"  :precision="60" @created="stopTimer"/>
            <TargetCircle :class="{red: true}"  :precision="80" @created="stopTimer"/>
            <TargetCircle :class="{yellow: true}"  :precision="100" @created="stopTimer"/>
        </div>

</template>

<script>
import TargetCircle from './TargetCircle.vue'

export default {
    name: 'Target',
    components: { TargetCircle },
    props: ['delay'],
    data() {
        return {
            showTarget: false,
            timer: null,
            reactionTime: 0,
            precisionTarget: 0,

            // Register the device resolution width & generate a random position for the target
            displayWidth: screen.width,
            positionX:  Math.random() * 70,
            positionY: Math.random() * 30
            
        }
    },
    mounted() {
        setTimeout(() => {
            this.showTarget = true
            this.startTimer()
        }, this.delay)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10)
        },
        stopTimer(precisionCircle) {
            clearInterval(this.timer)
            this.precisionTarget = precisionCircle
            let resultsObj = {ReactTime: this.reactionTime, Target: this.precisionTarget}
            this.$emit('end', resultsObj)

            // console.log("reactionTime " +  this.reactionTime);
        },
    },
    // For a width of below 500px reduces the horizontal interval for the target position
    created() {
        if(this.displayWidth < 500) {
            this.positionX = this.positionX
            this.positionY =  this.positionY
        }
        else {
            this.positionX = this.positionX * 0.6
            this.positionY =  this.positionY  * 0.9
        }
    }
}
</script>

<style>
    .container {
        position: relative;
        padding: 0;
        width: 90%;
        height: 450px;
        margin: auto;
    }
    .target-container {
        position: relative;
        top: 10%;      
        display: flex;
        justify-content: center;
        align-items: center;
        width: 300px;
        height: 300px;
        border-radius: 50%;
        border: 1px solid black;
        box-shadow: 3px 5px 10px black;
        z-index: 1;
    }
    .target {
        position: absolute;
        border-radius: 50%;
    }
    .white {
        width: 100%;
        height: 100%;
        background-color: white;
        z-index: 5;
    }
    .black {
        width: 80%;
        height: 80%;
        background-color: black;
        z-index: 6;
    }
    .blue {
        width: 60%;
        height: 60%;
        background-color: blue;
        z-index: 7;
    }
    .red {
        width: 40%;
        height: 40%;
        background-color: red;
        z-index: 8;
    }
    .yellow {
        width: 20%;
        height: 20%;
        background-color: yellow;
        z-index: 9;
    }

    .visible {
        display: flex;
    }

    @media screen and (max-width: 600px) {
        .target-container {
            width: 200px;
            height: 200px;
        }
    }
</style>