<template>
    <SearchFieldView v-on:add-node-workflow="addNodeWorkflow" v-bind:allNodes="allNodes" />
    <div class="work-flow-view">
        <WorkflowNode v-for="node in workflowNodes" v-bind:key="node.uiIdx" v-bind:node="node"/>
    </div>
</template>

<script>
    import SearchFieldView from './components/SearchFieldView.vue'
    import WorkflowNode from './components/WorkflowNode.vue'

    export default {
        name: 'App',
        components: {
            SearchFieldView,
            WorkflowNode
        },
        data() {
            return {
                allNodes: [],
                workflowNodes: []
            }
        },
        methods: {
            addNodeWorkflow(name) {
                console.log(this.allNodes)
                const filteredNodes = this.allNodes.filter(node => node.name === name)
                filteredNodes.forEach((ele, idx) => ele.id = idx + this.allNodes.length)
                this.workflowNodes = this.workflowNodes.concat(filteredNodes)
                console.log(this.workflowNodes)
            },
            getNodes() {
                let data = [
                    {
                        "name": "Excel Reader",
                        "icon": "bi bi-file-earmark-arrow-down"
                    },
                    {
                        "name": "CSV Reader",
                        "icon": "bi bi-file-earmark-arrow-down"
                    },
                    {
                        "name": "Excel Writer",
                        "icon": "bi bi-file-earmark-arrow-up"
                    },
                    {
                        "name": "CSV Writer",
                        "icon": "bi bi-file-earmark-arrow-up"
                    },
                    {
                        "name": "Sorter",
                        "icon": "bi bi-sort-down-alt"
                    },
                    {
                        "name": "Row filter",
                        "icon": "bi bi-filter"
                    },
                    {
                        "name": "Column filter",
                        "icon": "bi bi-filter"
                    },
                    {
                        "name": "Bar Chart",
                        "icon": "bi bi-bar-chart"
                    },
                    {
                        "name": "Scatter Plot",
                        "icon": "bi bi-bar-chart"
                    },
                    {
                        "name": "Parallel Coordinates Plot",
                        "icon": "bi bi-bar-chart"
                    },
                    {
                        "name": "Histogram",
                        "icon": "bi bi-bar-chart"
                    },
                    {
                        "name": "Naive Bayes Learner",
                        "icon": "bi bi-diagram-3"
                    },
                    {
                        "name": "Naive Bayes Predictor",
                        "icon": "bi bi-diagram-3"
                    },
                    {
                        "name": "DBSCAN",
                        "icon": "bi bi-grid-1x2-fill"
                    },
                    {
                        "name": "k-Means",
                        "icon": "bi bi-grid-1x2-fill"
                    },
                    {
                        "name": "Decision Tree Learner",
                        "icon": "bi bi-diagram-3"
                    },
                    {
                        "name": "Decision Tree Predictor",
                        "icon": "bi bi-diagram-3"
                    }
                ]
                const colors = ['#ff9999', '#ffcc99', '#b3e6b3']
                data.forEach(ele => {
                    ele.color = colors[Math.floor(Math.random() * colors.length)];
                })
                return data
            }
        },
        created() {
            this.allNodes = this.getNodes()
            if (this.allNodes.length <= 0) {
                return
            }
            this.workflowNodes = [{...this.allNodes[1]}, {...this.allNodes[6]}, {...this.allNodes[14]}, {...this.allNodes[8]}]
            const winHeight = 9/10 * window.innerHeight + 1
            const winWidth = 9/10 * window.innerWidth + 1
            this.workflowNodes.forEach((node, idx) => {
                node.top = `${2 / 4 * winHeight}px`
                node.left = `${(idx + 1)  / 8 * winWidth}px`
                node.id = idx
            })
            console.log(this.workflowNodes)
        }
    }
</script>

<style>
.work-flow-view {
    height: 100%;
    width: 100%;
    display: table;
    margin: 0 auto;
}
</style>
