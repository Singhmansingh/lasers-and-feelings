<template>
    <div id="container">
        <screen-component/>
        <player-component/>
    </div>
</template>

<script>
import ScreenComponent from './SceenComponent.vue'
import PlayerComponent from './PlayerComponent.vue'
export default {
    name: "GameScreen",
    components:{
        ScreenComponent,
        PlayerComponent
    }
}
</script>

<style lang='scss' scoped>
    #container {
        flex:1;
        justify-content: center;
        display: flex;
        flex-direction: column;
    }
</style>