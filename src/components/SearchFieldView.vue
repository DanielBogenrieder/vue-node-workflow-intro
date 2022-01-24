<template>
    <div class="search-field-view" v-on:mouseover="mouseOverSearch" v-on:mouseleave="mouseLeaveSearch">
        <input v-on:keyup="filterResults" v-model="inputChars" type="text" placeholder="Add new node..." list="possibleNodes">
        <ul class="dropdown-content" v-if="showPossibleNodes && this.localNodes.length > 0" id="possibleNodes">
            <li v-for="node in localNodes" v-bind:key="node.name.replace(' ','_')" v-on:click="nodeClick(node)">{{ node.name }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'SearchFieldView',
    props: {
        allNodes: Array
    },
    data() {
        return {
            localNodes: this.allNodes.map(node => ({...node})),
            showPossibleNodes: false,
            inputChars: ''
        }
    },
    methods: {
        mouseOverSearch() {
            this.localNodes = this.allNodes.filter(node => node.name.toLowerCase().includes(this.inputChars.toLowerCase()))
            this.showPossibleNodes = true
        },
        mouseLeaveSearch() {
            this.showPossibleNodes = false
        },
        filterResults() {
            this.localNodes = this.allNodes.filter(node => node.name.toLowerCase().includes(this.inputChars.toLowerCase()))
        },
        nodeClick(node) {
            this.inputChars = ''
            this.showPossibleNodes = false
            this.$emit('add-node-workflow', node.name)
        }
    }
}
</script>

<style scoped>
.search-field-view {
    display: table;
    margin: 0 auto;
    padding: 0pt 0pt 1vh 0pt;
}

input {
    margin: 1vh 1vw 0vh 1vw;
    width: 20vw;
    height: 2vh;
    min-height: 20px;
    font-size: 12pt;
    border: solid black 2pt;
}

.dropdown-content {
    margin: 0.4vh 1vw 0vh 1vw;
    padding: 0pt 2pt 2pt 2pt;
    display: block;
    position: absolute;
    background-color: lightgray;
    min-width: 20vw;
    overflow: auto;
    z-index: 10;
}

ul {
    margin: 0;
    padding: 0;
}

li:hover {
    background-color: darkgray;
}
</style>