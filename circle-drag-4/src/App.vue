<template>
  <div id='arc'>

  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  name: "App",
  data() {
    return {
      width: 1920,
      height: 1080,
      radius: 40,
      circlesData: null,
      svg: null,
      g: null,
      drag_handler: null
    };
  },

  mounted() {
    // this.circlesData = d3.range(20).map(i => ({
    //   x: Math.random() * (this.width - this.radius * 2) + this.radius,
    //   y: Math.random() * (this.height - this.radius * 2) + this.radius,
    // }));

    this.circlesData = [
      {x: 280, y: 80},
      {x: 80, y: 280},
      {x: 280, y: 280},
      {x: 480, y: 280},
      {x: 280, y: 480},

      // {x: 780, y: 80},
      // {x: 580, y: 280},
      // {x: 780, y: 280},
      // {x: 980, y: 280},
      // {x: 780, y: 480},

    ]

    console.log(this.circlesData)

    this.createSVG()
    
    /*
    this.svg = d3
        .select('#arc')
        .append('svg')
        .attr('width', this.width)
        .attr('height', this.height)
        .attr("stroke-width", 2);

    let circles = this.svg.selectAll("circle")
        .data(this.circlesData)
        .enter()
        .append('circle')
        .attr('cx', d => d.x)
        .attr('cy', d => d.y)
        .attr('r', this.radius)
        .attr('fill', (d, i) => d3.schemeCategory10[i % 10])

    function dragmove(event, d) {
      console.log(event.x)
          d.x = event.x
          d.y = event.y
          d3.select(this)
            .attr('cx', d.x = event.x)
            .attr('cy', d.y = event.y)
    }
    
    let dragHandler = d3.drag()
        .on('drag', dragmove)
    
    dragHandler(circles)
    */

  },

  methods: {
    
    createSVG() {
      let width = window.innerWidth,
          height = window.innerHeight;

      this.svg = d3
        .select('#arc')
        .append('svg')
        .attr('width', width)
        .attr('height', height)
        .attr("stroke-width", 2);

      this.circlesRequest();
    },

    circlesRequest() {
      let that = this;
      let circles = this.svg.selectAll("circle")
        .data(this.circlesData)
        .enter()
        .append('circle')
        .attr('cx', d => d.x)
        .attr('cy', d => d.y)
        .attr('r', this.radius)
        .attr('fill', (d, i) => d3.schemeCategory10[i % 10])

      this.dragHandler = d3.drag()
        .on('drag', function(event, d){
          d3.select(this)
            .attr('cx', d.x = event.x)
            .attr('cy', d.y = event.y)
        })
    
      this.dragHandler(circles)

    },

    dragmove(event, d) {
      console.log(event.x)
          d.x = event.x
          d.y = event.y
          // this !!
          d3.select(this)
            .attr('cx', d.x = event.x)
            .attr('cy', d.y = event.y)
    }
    

  }
}
</script>

<style>

</style>
