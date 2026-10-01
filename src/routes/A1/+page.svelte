<script lang='ts'>
   import * as d3 from "d3";
   type Datum = { name: string; value: number };

   let data: Datum[] = $state([
       { name: "A", value: 23 },
       { name: "B", value: 69 },
       { name: "C", value: 46 },
       { name: "D", value: 115 }
   ]);
   const pie = d3
       .pie<Datum>()
       .padAngle(3 / 100)
       .sort(null)
       .value((d) => d.value);

   const arcGen = d3.arc().innerRadius(40).outerRadius(100);

   const colorScale = d3
       .scaleOrdinal(d3.schemeTableau10)
       .domain(data.map((d) => d.name));
</script>

<svg height="400" width="600">
   <g transform="translate(200, 150)">
       {#each pie(data) as d}
           <path fill={colorScale(d.data.name)} d={arcGen(d)} />
           <text
                transform="translate({arcGen.centroid(d)})"
                text-anchor="middle"
                fill="white"
                font-size="12px"
                font-weight="bold">
                {d.data.name}: {d.data.value}
            </text>
       {/each}
   </g>
</svg>
