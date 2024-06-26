<script>
  import { onMount } from "svelte";
  import { shapes } from "$lib/shapes.js";

  export let card;
  let angle = 0;
  $: shape = decodeURIComponent(shapes[card.split("-")[1]]);

  let width = 0;
  let top = "100vh";
  let left = "-50vw";

  onMount(() => {
    setTimeout(() => {
      width = 120;
      top = "0px";
      left = "0px";
      angle = 360 + Math.random() * (Math.random() > 0.5 ? 1 : -1) * 20;
    }, 200);
  });
</script>

<div
  class="transition-all duration-1000 max-w-[1/3] ease-out relative h-[150px] md:h-[200px]"
  style={`width: ${width}px;`}
>
  <div
    class={`bg-slate-100 rounded-3xl shadow-lg left w-full h-full absolute transition-all duration-1000`}
    style={`top: ${top}; left: ${left}; transform: rotate(${angle}deg);`}
  >
    <div class="relative h-full flex items-center justify-center">
      <p class="text-black font-bold text-2xl text-center">{card}</p>
      <span
        class="text-[40px] {(shape == '&#x2663;') | (shape == '&#x2660;')
          ? 'text-black'
          : 'text-red-700'} absolute top-[2px] left-2">{@html shape}</span
      >
    </div>
  </div>
</div>
