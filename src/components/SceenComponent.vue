<template>
    <div id="screen-container">
        <div id="screen">
            <h1  @click="openRules">Lasers and Feelings!</h1>
            <h2 class="section">Mission Statement:</h2>
            <div class="status-container">
                <h3 class="mission" contenteditable="true" spellcheck="false">Do awesome Space stuff!</h3>
            </div>
            <h2 class="section">Raptor Status:</h2>
            <div class="status-container">
                <h3 v-for="(activeStrength, index) in activeStengths" :key="'strength-'+index" @click="changeStrength(index)">
                    {{strengths[activeStrength].system}}: <span class="good">Online!</span>
                </h3>
            </div>
            <h2 class="section">Warning:</h2>
            <div class="status-container">
                <h3 :title="problems[activeWeakness].info" @click="changeWeakness">{{problems[activeWeakness].system}}: <span class="bad">{{problems[activeWeakness].status}}</span> </h3>
            </div>
        </div>
    </div>
</template>

<script>
import * as DATA from './data.json';
export default {
    name:"ScreenComponent",
    setup(){
        const strengths = DATA.strengths;
        const problems = DATA.problems;
        return {
            strengths,
            problems
        }
    },
    data(){
        return {
            activeStengths:[0,1],
            activeWeakness:0
        }
    },
    methods:{
        changeStrength(activeStrengthIndex){
            console.log(activeStrengthIndex, this.strengths.length)
            if(this.activeStengths[activeStrengthIndex] < this.strengths.length-1) this.activeStengths[activeStrengthIndex]++ ;
            else this.activeStengths[activeStrengthIndex] = 0;
        },
        changeWeakness(){
            if(this.activeWeakness < this.problems.length-1)this.activeWeakness++;
            else this.activeWeakness = 0;
        },
        openRules(){
            window.open("http://onesevendesign.com/lasers_and_feelings_rpg.pdf","_blank")
        }
    }
}
</script>

<style lang="sass" scoped>

$blue:#88c4ff
$grey:rgb(25,25,25)
#screen-container
    flex-shrink:1
    width: 100%
    align-items: center
    display: flex
    justify-content: center
    padding-top: 10px
    padding-bottom: 10px
   
#screen 
    width: 800px
    min-height: 450px
    font-family: "Title"
    border-radius: 5px
    border: 8px inset darken($grey, 90%)
    height: 90%
    color: $blue
    display: flex
    box-sizing: border-box
    flex-direction: column
    background-color: $grey
    font-size: 1.2em
    letter-spacing: 2px
    .section 
        color: orange
        font-size: 1em
    .good
        color:#00ff00

    .good,.bad
        font-size: 0.8em
    .bad
        color:#ff0000
    h1
        font-size: 3em
        flex:1
        margin:10px
        cursor: pointer

    h2
        flex-shrink:1
        margin:0

    .mission
        font-size:1.4em
        user-select: text !important
        cursor: text !important

    .status-container
        display: flex
        flex-direction: row
        justify-content: space-evenly
        flex:1
        h3
            flex:1
            user-select: none
            cursor: pointer
            transition: all 0.3s ease



    
</style>