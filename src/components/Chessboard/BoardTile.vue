<template>
    <div :class="tileColorStr" @click="selectPiece">
        <div class="sizeContent">
            <img class="sizeContent" v-if="imageStr" :src="imageStr" alt="" draggable="false"/>
        </div>
    </div>
</template>

<style scoped>
    .sizeContent {
        height: 100%;
        width: 100%;
    }
    .sizeContent img {
        height: 100%;
        width: 100%;
    }
    .whiteTile {
        background-color: rgb(170, 220, 180);
        color: black;
    }
    .blackTile {
        background-color: rgb(50, 130, 85);
        color: white;
    }
    .selectedTile {
        background-color: rgb(230, 220, 60);
    }

</style>

<script setup>
import { computed } from 'vue';

    const props = defineProps({
        index: {
            type: Number,
            required: true
        },
        cordinates: {
            type: Array,
            required: true
        },
        isWhite: {
            type: Boolean,
            required: true
        },
        pieceInfo: {
            type: Array,
            required: false
        },
        isSelected: {
            type: Boolean,
            required: false,
            default: false
        }
    })

    const emits = defineEmits(['selectPiece'])
    const tileColor = (props.isWhite ? "whiteTile" : "blackTile")
    const tileColorStr = computed(() => {return props.isSelected ? "selectedTile" : tileColor})
    const x = props.cordinates[0]
    const y = props.cordinates[1]
    const imageStr = computed(() => {
        let str = null
        if(props.pieceInfo == null)
            return str;
        if(props.pieceInfo[0] == "w") {
            switch (props.pieceInfo[1]) {
                case "R":
                    str = "/images/Chess_rlt60.png"
                    break;
                case "N":
                    str = "/images/Chess_nlt60.png"
                    break;
                case "B":
                    str = "/images/Chess_blt60.png"
                    break;
                case "Q":
                    str = "/images/Chess_qlt60.png"
                    break;
                case "K":
                    str = "/images/Chess_klt60.png"
                    break;
                case "p":
                    str = "/images/Chess_plt60.png"
                    break;
            }
        } else if(props.pieceInfo[0] == "b") {
            switch (props.pieceInfo[1]) {
                case "R":
                    str = "/images/Chess_rdt60.png"
                    break;
                case "N":
                    str = "/images/Chess_ndt60.png"
                    break;
                case "B":
                    str = "/images/Chess_bdt60.png"
                    break;
                case "Q":
                    str = "/images/Chess_qdt60.png"
                    break;
                case "K":
                    str = "/images/Chess_kdt60.png"
                    break;
                case "p":
                    str = "/images/Chess_pdt60.png"
                    break;
            }
        }
        return str
    })

    function selectPiece() {
        emits('selectPiece', {
            pieceInfo: props.pieceInfo,
            index: props.index
        })
    }
</script>