<template>
    <div class="boardGrid">
        <BoardTile v-for="tile in tiles" :cordinates="tile.cordinates" :is-white="tile.isWhite" :piece-name="tile.pieceName"/>
    </div>
</template>

<style>
    .boardGrid {
        display: grid;
        grid-template-columns: repeat(8, 120px);
        grid-template-rows: repeat(8, 120px);
        width: fit-content;
        height: fit-content;
    }
</style>

<script setup>
import BoardTile from './BoardTile.vue';

    const props = defineProps({
        hasWhite: {
            type: Boolean,
            required: true
        },
        position: {
            type: Map,
            required: true
        }
    })

    let tiles = []
    let tileColor = true
    let cordinatesX = Array[8]
    let cordinatesY = Array[8]

    if(props.hasWhite) {
        cordinatesX = ['a','b','c','d','e','f','g','h']
        cordinatesY = ['8','7','6','5','4','3','2','1']
    } else {
        cordinatesX = ['h','g','f','e','d','c','b','a']
        cordinatesY = ['1','2','3','4','5','6','7','8']
    }
    
    for(let i = 0; i < 8; i++) {
        const y = cordinatesY[i]
        for(let j = 0; j < 8; j++) {
            const x = cordinatesX[j]

            let pieceName = props.position.get(x+y)
            if(!pieceName) {
                pieceName = "none"
            }
            console.log(pieceName);

            let tile = {
                cordinates: [x,y],
                isWhite: tileColor,
                pieceName: pieceName
            }
            tiles.push(tile)
            if(j%8 != 7)
                tileColor = !tileColor
        }
    }

</script>