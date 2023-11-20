<template>
    <div class="boardGrid">
        <BoardTile v-for="tile in tiles" :index="tile.index" :cordinates="tile.cordinates" :is-white="tile.isWhite" :piece-info="tile.pieceInfo" :is-selected="tile.isSelected" @selectPiece="handleSelectPiece"/>
    </div>
</template>

<style>
    .boardGrid {
        display: grid;
        grid-template-columns: repeat(8, 100px);
        grid-template-rows: repeat(8, 100px);
        width: fit-content;
        height: fit-content;
    }
</style>

<script setup>
import { ref } from 'vue';
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

    let selectedTileIndex = null
    let tiles = ref([])
    let tileColor = true
    let cordinatesX = Array[8]
    let cordinatesY = Array[8]

    // Creating cordinates in an order based on player color
    // This seemed easier than flipping the direction the tiles were created
    if(props.hasWhite) {
        cordinatesX = ['a','b','c','d','e','f','g','h']
        cordinatesY = ['8','7','6','5','4','3','2','1']
    } else {
        cordinatesX = ['h','g','f','e','d','c','b','a']
        cordinatesY = ['1','2','3','4','5','6','7','8']
    }
    
    // Creating the array of tiles based on the given position
    for(let i = 0; i < 8; i++) {
        const y = cordinatesY[i]
        for(let j = 0; j < 8; j++) {
            const x = cordinatesX[j]

            let pieceInfo = props.position.get(x+y)

            let tile = {
                index: i*8+j,
                cordinates: [x,y],
                isWhite: tileColor,
                pieceInfo: pieceInfo
            }
            tiles.value.push(tile)
            if(j%8 != 7)
                tileColor = !tileColor
        }
    }

    function handleSelectPiece(data) {
        if(selectedTileIndex != null){
            if(selectedTileIndex != data.index){
                tiles.value[data.index].pieceInfo = tiles.value[selectedTileIndex].pieceInfo
                tiles.value[selectedTileIndex].pieceInfo = null
            }
            tiles.value[selectedTileIndex].isSelected = false
            selectedTileIndex = null
        }
        else if(data.pieceInfo){
            selectedTileIndex = data.index
            tiles.value[data.index].isSelected = true
        }
    }

</script>