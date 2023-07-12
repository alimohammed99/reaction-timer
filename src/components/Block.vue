<template>
    <div title="Click quickly. Hurry!!!" class="block" v-if="showBlock" @click="stopTimer">
    
    
    
    
    
    
    
        Click me
    
    
    
    
    
    
    
    </div>
</template>

<script>
export default {
    props: ['delay'],
    // delay is on the parent(app.vue) component. So we are receiving it here as a property coz we wanna use it here.
    // properties are declared(as normal data objects) in the "app.vue" file and they are used in the subComponents(children components) as props.
    // But you need to register the children components inside the "app.vue" by importing them there and also add them to the components.
    // Now you can use the children-component and also the props inside the parent-component by writing the name of the children components in the form of a self-closing tag while you bind the prop to it.
    data() {
        return {
            showBlock: false,
            timer: null,
            // The Timer itself
            reactionTime: 0
            // The amount of time it takes users to click the square
        }
    },
    mounted() {
        console.log('Component has been mounted')
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
        }, this.delay)
        // setTimeout(() => {action}, time)
        // setInterval(() => {action}, time)
        // clearInterval(action)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10);
        },
        // "timer" stores a particular interval that runs every 10 millisecs, and for every 10 millisecs, "reactionTime" is gonna be increased by 10 millisecs.
        stopTimer() {
            clearInterval(this.timer)
            console.log(this.reactionTime)
            this.$emit('end', this.reactionTime)
            // Because I need to send data(this.reactionTime) from this child component(Block.vue) to the Parent Component(App.vue) before I can now display to users.
            //N:B- 'end' is custom. Can be anything.
        }
    },
    updated() {
        console.log('Component has been updated')
    },
    unmounted() {
        console.log('Component has been unmounted')
    }
}
</script>

<style scoped>
.block {
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
    font-size: 30px;
    border: 7px dashed blue;
    cursor: pointer;
}
</style>