<template>
  <div id="app">
    <h1>d3 visualization within vue</h1>
    <svg width="800" height="600" id="viz"></svg>

  </div>
</template>

<script>
const d3 = require('d3')

export default {
  name: 'App',
  components: {

  },
  mounted(){
    let numbers = [100, 250, 160, 80, 200]

    // select visual environment
    const svg = d3.select('#viz');


    const scaleLength = d3.scaleLinear()
      .domain([0, d3.max(numbers)])
      .range([0, 600]);

    const scalePos = d3.scaleBand()
      .domain(d3.range(numbers.length))
      .range([0, 300])
      .paddingInner(0.05)
      .paddingOuter(0.05);

    //======== Create g groups =========

    const gs = svg.selectAll('g.bars')
      .data(numbers)
      .join('g').attr('class', 'bars');

    gs.attr('transform', (d, i) => `translate(0, ${scalePos(i)})`);

    gs.append('rect')
      .attr('height', scalePos.bandwidth())
      .attr('width',scaleLength)
        .attr('fill', '#0a1f89');

    gs.append('text')
      .text((d) => d)
        .attr('x', scaleLength)
    .attr('y',scalePos.bandwidth()/2);


  }


}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
