<template>
    <div ref="draggableDiv" v-on:mousedown="dragElement" v-bind:style="[node.hasOwnProperty('top') ? {'background-color': node.color, 'top': node.top, 'left': node.left} : {'background-color': node.color, 'top': '50px', 'left': '50px'}]">
        <h6>{{ node.name }}</h6>
        <i v-bind:class="node.icon"></i>
    </div>
</template>

<script>
import "bootstrap-icons/font/bootstrap-icons.css";

export default {
    name: 'WorkflowNode',
    props: {
        node: Object
    },
    data() {
        return {
            positions: {
                clientX: undefined,
                clientY: undefined,
                movementX: 0,
                movementY: 0
            }
        }
    },
    methods: {
        dragElement(e) {
            e.preventDefault()
            this.positions.clientX = e.clientX
            this.positions.clientY = e.clientY
            document.onmousemove = this.elementDrag
            document.onmouseup = this.closeDragElement
            },
        elementDrag(event) {
            event.preventDefault()
            this.positions.movementX = this.positions.clientX - event.clientX
            this.positions.movementY = this.positions.clientY - event.clientY
            this.positions.clientX = event.clientX
            this.positions.clientY = event.clientY
            this.$refs.draggableDiv.style.top = (this.$refs.draggableDiv.offsetTop - this.positions.movementY) + 'px'
            this.$refs.draggableDiv.style.left = (this.$refs.draggableDiv.offsetLeft - this.positions.movementX) + 'px'
            },
        closeDragElement() {
            document.onmouseup = null
            document.onmousemove = null
        }
    }
}
</script>

<style scoped>
div {
    border: solid 2pt black;
    padding: 2pt;
    position: absolute;
    z-index: 5;
    min-width: 75px;
    text-align: center;
}

</style>