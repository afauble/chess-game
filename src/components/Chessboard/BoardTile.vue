<template>
    <div :class="tileColorStr">
        <div class="center">
            {{ props.pieceName }}
        </div>
    </div>
</template>

<style scoped>

    .center {
        position: relative;
        float: left;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .whiteTile {
        background-color: white;
        color: black;
    }

    .blackTile {
        background-color: black;
        color: white;
    }

</style>

<script setup>
    const props = defineProps({
        cordinates: {
            type: Array,
            required: true
        },
        isWhite: {
            type: Boolean,
            required: true
        },
        pieceName: {
            type: String,
            required: false
        }
    })

    const tileColorStr = (props.isWhite ? "whiteTile" : "blackTile")
    const x = props.cordinates[0]
    const y = props.cordinates[1]
</script>