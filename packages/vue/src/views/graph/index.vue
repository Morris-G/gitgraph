<template>
  <div class="git-graph">
    <h3>Git Graph</h3>
    <div id="graphArea" class="graph-area"></div>
  </div>
</template>

<script>
import { createGitgraph, templateExtend } from '@gitgraph/js'
import gitflow from './gitflow'
import docLog from './export'

export default {
  data() {
    return {}
  },
  mounted() {
    const graphContainer = document.getElementById('graphArea')

    // Instantiate the graph.
    const gitgraph = createGitgraph(graphContainer, {
        // mode: 'compact'
        orientation: 'vertical',
        template: templateExtend('metro', {
            colors: ['#6997ff', '#30D878', '#FF5630', '#081e40'],
            arrow: {
                // size: 4,
                // offset: 0
            },
            branch: {
                lineWidth: 2,
                spacing: 10,
                label: {
                    display: true,
                    font: 'normal 14px Avenir, Helvetica, Arial, sans-serif',
                    // color: '#ffffff',
                    // bgColor: 'rgba(0, 0, 0, .5)',
                    // strokeColor: 'transparent'
                },
                mergeStyle: 'bezier'
            },
            commit: {
                // spacing: 30,
                message: {
                    color: '#2e2e2e',
                    displayHash: false,
                    displayAuthor: true,
                    font: 'normal 14px Avenir, Helvetica, Arial, sans-serif'
                },
                dot: {
                    size: 4,
                    strokeWidth: 2
                }
            },
            tag: {
                color: '#2e2e2e',
                bgColor: 'transparent',
                font: 'normal 12px Avenir, Helvetica, Arial, sans-serif',
                borderRadius: 5,
                pointerWidth: 6
            }
        })
        
    })
		// gitgraph.import(gitflow)
		// gitgraph.import(docLog)

    
		// Simulate git commands with Gitgraph API.
    const master = gitgraph.branch('master')
    master.commit('Initial commit')

    const develop = gitgraph.branch('develop')
    develop.commit('Add TypeScript')

    const aFeature = gitgraph.branch('a-feature')
    aFeature.commit('Make it work').commit('Make it right').commit('Make it fast')

    develop.merge(aFeature)
    develop.commit('Prepare v1')

    master.merge(develop).tag('v1.0') 
		
  },
  methods: {},
}
</script>

<style lang="scss" scoped>
.graph-area {
    padding: 0 100px;
    text-align: left;
}
</style>