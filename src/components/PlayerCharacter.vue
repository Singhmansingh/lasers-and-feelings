<template>
<div class="character-container" :style="{marginTop: margin+'px'}">
 <div id="player" @click="togglePopover">
     <p id="player-title" :style="{backgroundColor:roles[role].colorPrimary, color:roles[role].colorSecondary}">{{displayedName}}</p>
    </div>

    <Transition name="popout">
<div id="popover" v-show="playerStatsVisible" :class="{secondHalf: secondHalf}">
        <div class="header">
            <p ref="nameBar" contenteditable="true" spellcheck="false">{{displayedName}}</p>
        </div>
        <div class="body">
             <div class="section">
                <p>Role</p>
                <select class="selection" @change="setRole" ref="roleSelector">
                    <option v-for="(role,index) in roles" :key="'style='+role.name" :value="index">{{role.name}}</option>
                </select>
            </div>
            <div class="section">
                <p>Style</p>
                <select class="selection">
                    <option v-for="style in styles" :key="'style='+style.name" :value="style.name">{{style.name}}</option>
                </select>
            </div>
             <div class="section">
                <p>Laser-Feelings Rating</p>
                <div class="laser-feelings" v-on:click.left="increaseLaser" v-on:click.right="increaseFeeling" @contextmenu="e => e.preventDefault()">
                    <div class="laser-feeling-bar" :style="{width: ((laserFeelingScale)/6)*100 + '%'}">{{laserFeelingScale}}</div>
                </div>
            </div>
           
        </div>
    </div>
    </Transition>
    
</div>
   
</template>

<script>
import * as DATA from './data.json';

export default {
    name:"PlayerCharacter",
    setup(){
        const roles = DATA.roles;
        const styles = DATA .styles;
        return {
            roles,
            styles
        }
    },
    props:{
        id:Number,
        margin:Number,
        secondHalf: {
            type: Boolean,
            default: false
        }
    },
    mounted(){
        this.$refs.nameBar.addEventListener('input', (e) => {
                this.name=e.target.textContent
            })
    },
    data(){
        return{
            laserFeelingScale: 3,
            name: "",
            displayedName:"Captain John Stud",
            role: 0,
            style: 0,
            goal:0,
            playerStatsVisible: false,
            equiptment:["Consortium Uniform","Space Mobile Communicator & Scanner device thing","variable beam phase pistol stunner"]
        }
    },
    methods:{
        togglePopover(){
            if(this.playerStatsVisible) this.closePopover();
            else this.playerStatsVisible = true;
        },
        increaseLaser(){
            if(this.laserFeelingScale < 5) this.laserFeelingScale++;
        },
        increaseFeeling(){
            if(this.laserFeelingScale > 2) this.laserFeelingScale--;
        },
        closePopover(){
            if(!this.name) this.name = this.displayedName;
            else this.displayedName = this.name;
            this.playerStatsVisible = false;
        },
        setRole(){
            this.role = this.$refs.roleSelector.value
        }
    }
}
</script>

<style lang="sass" scoped>

$playerwidth: 150px
$playerheight: 250px

$popoverWidth: 380px
$popoverHeight: 370px


$popoverBackground: none
$popoverHeaderBackground: #0054a8
$popoverBodyBackground: white
$laserFeelingBarBackground: #e4e4e4
$laserFeelingBar: #0080ff



.character-container
    display: flex
    justify-content: center
    align-items: center
    position: relative
    flex-direction: row
    position:fixed
#player
    width: $playerwidth
    height: $playerheight
    cursor: pointer
    flex:1
    background-image: url('../assets/person.png')
    background-size: contain
    background-repeat: no-repeat
    background-position: center
    user-select: none
    font-family: "Name"
    font-weight: bold
    font-size: 1.25em
    color: white
    display: flex
    align-items: flex-end
    justify-content: center
    
    #player-title 
        margin: 0
        margin-bottom: - 70px
        padding: 5px
        min-width: 200px
        min-height: 50px
        justify-content: center
        align-items: center
        display: flex
        background: $popoverHeaderBackground
        border-radius: 10px
        transition: all 0.3s ease

    
#popover
    width: $popoverWidth
    font-family: "Name"
    height: $popoverHeight
    border-radius: 20px
    overflow: hidden
    flex: 1
    position: absolute
    background: $popoverBackground
    left: calc($playerwidth + 10px)
    z-index: 4
    display: flex
    flex-direction: column
 
    .header
        flex-shrink:1
        background:$popoverHeaderBackground
        padding: 15px
        font-size: 1.5em
        font-weight: bold
        letter-spacing: 2px
        p
            margin:0
            color: white
            transform: skew(-13deg)
    .body
        flex:1
        background: $popoverBodyBackground
        display: flex
        flex-direction: column
        align-items: flex-start
        padding: 20px
        .section
            p 
                margin: 5px
                font-size: 1.15em
                transform: skew(-13deg)
            flex:1
            text-align: left
            width: 100%
            .selection
                width: 100%  
                font-size: 1.25em
                background: none
                border-width: 0 0 2px 0 
                border-style: dashed
                border-color: black
                font-family: inherit

                option 
                    font-size: 0.75em
        .laser-feelings
            width: 100%
            height: 40px
            background: $laserFeelingBarBackground
            border-radius: 30px
            overflow: hidden
            cursor: pointer
            user-select: none
            .laser-feeling-bar
                background: $laserFeelingBar
                height: 100%
                justify-content: center
                align-items: center
                display: flex
                color: white
                transition: width 0.5s ease

.secondHalf
    left: calc(-2.8* $playerwidth + 10px) !important

.popout-enter-active
    animation: popout 0.4s ease
.popout-leave-active 
    animation: popout 0.4s ease reverse


@keyframes popout
    0%

        transform: scaleX(0) scaleY(0.05)
        opacity:0
    
    50%
        transform: scaleX(1)  scaleY(0.1)  
    100%
        
        transform: scaleY(1)
                 opacity: 1


</style>