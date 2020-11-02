<template>
  <div>
    <h1>Circle Pack in D3</h1>
    <h2>{{ msg }}</h2>
    <div id='svg-container'>

    </div>
  </div>
</template>

<script>
import * as d3 from "d3";
// import {nest} from 'd3-collection';
export default {
  name: "CircleChart",
  props: ["tweetData"],
  data() {
    return {
      msg: "👋 from the Chart Component",
      height: 600,
      width: 600,
      radius: 32
    };
  },

  mounted() {
      this.packChart();
  },

  methods: {
    packChart() {
        const svg = d3.create("svg")
        .attr("viewBox", [0, 0, this.width, this.height])
        .attr("stroke-width", 2);

        const circles = d3.range(20).map(i => ({
            x: Math.random() * (this.width - this.radius * 2) + this.radius,
            y: Math.random() * (this.height - this.radius * 2) + this.radius,
        }));

        svg.selectAll("circle")
            .data(circles)
            .join("circle")
            .attr("cx", d => d.x)
            .attr("cy", d => d.y)
            .attr("r", this.radius)
            .attr("fill", (d, i) => d3.schemeCategory10[i % 10])
            .call(this.drag);

        const container = d3.select('#svg-container');
        container.append(svg)
        
        // return svg.node();
    
    },

    drag() {
        function dragstarted(event, d) {
            d3.select(this).raise().attr("stroke", "black");
        }

        function dragged(event, d) {
            d3.select(this).attr("cx", d.x = event.x).attr("cy", d.y = event.y);
        }

        function dragended(event, d) {
            d3.select(this).attr("stroke", null);
        }

        return d3.drag()
            .on("start", dragstarted)
            .on("drag", dragged)
            .on("end", dragended);
        }
  },
  computed: {
    
  }
};
</script>

<style>
</style>