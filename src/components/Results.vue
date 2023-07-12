<template>
    <p style="font-size:30px; text-decoration: ;">
    
        REACTION TIME: {{ score }} <span style="color:blue">milliseconds</span></p>
    
    
    
    <p class="rank" style="text-decoration:; font-style: italic; color:darkmagenta; background:; font-size:40px; font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif">Rank: {{ rank }}</p>
</template>

<script>
export default {

    props: ['score'],

    data() {
        return {
            rank: null
        }
    },
    mounted() {
        if (this.score < 250) {
            this.rank = 'NINJA FINGERS...'
        } else if (this.score < 400) {
            this.rank = 'RAPID FLEXES....'
        } else {
            this.rank = 'SNAIL PACE...'
        }
    }
}
</script>

<style scoped>
.rank {
    font-size: 1.4rem;
    color: #0faf87;
    font-weight: bold;
}
</style>