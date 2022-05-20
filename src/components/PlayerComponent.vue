<template>
    <div id="player-component-container">
        <div class="floor"/>
        <PlayerCharacter v-for="player in players" :key="'player-'+player" :margin="margins[player]" :id="player" :secondHalf="player*2 > players+1 ? true : false"/>
    </div>
</template>

<script>
import PlayerCharacter from './PlayerCharacter.vue'
export default {
    name:"PlayerComponent",
    components:{
        PlayerCharacter
    },
    data(){
        return{
            players: 1,
            margins:[]
        }
    },
    created(){
        this.calculateMargins()
    },
    mounted(){
        window.addEventListener('keyup', e => {
            if(e.key =="[" && this.players > 1) this.players--;
            else if(e.key =="]" && this.players < 9) this.players++;

            if(e.key == "]" || e.key =="[")this.calculateMargins();
        })
    },
    methods:{
        calculateMargins(){
            this.margins=[]
            for(let x = 0; x <= this.players; x++){
                let a = -1 * (3/this.players);
                let h = (this.players+1)/2;
                let k = this.players/6 - 1;
                console.log('h',h)
                let margin = a*((x-h)*(x-h)) + k
                this.margins.push(margin*70)
            }

            console.table(this.margins)
        }
    }
}
</script>

<style lang="sass" scoped>
#player-component-container 
    flex:2
    justify-content: space-around
    box-sizing: border-box
    align-items: center
    display: flex
    position: relative
    background-color: white
    border-top: 4px groove #454545
.floor
    width:100%
    height: 100%
    
    position: absolute
    box-sizing: border-box
    background-image: url('../assets/tile.png')
    opacity: 0.2
    transform-origin: top right 
</style>
