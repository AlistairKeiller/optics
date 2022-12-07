<script>
  import "uno.css";
  import "@unocss/reset/tailwind.css";
  let phasors = 100,
    totalAngle = Math.PI,
    path,
    currentX,
    currentY;
  var i;
  $: for (
    currentX = 150, currentY = 150, path = `M${currentX} ${currentY} `, i = 0;
    i < phasors;
    i++
  ) {
    currentX += (150 / phasors) * Math.cos((totalAngle * i) / phasors);
    currentY += (150 / phasors) * Math.sin((totalAngle * i) / phasors);
    path += `L${currentX} ${currentY} `;
  }
</script>

<div class="bg-neutral-2 @dark:bg-neutral-8" />
<svg class="fixed w-screen h-screen" viewBox="0 0 300 300">
  <path stroke="#0284c7" stroke-width="2" fill="none" d={path} />
  <circle
    cx={currentX}
    cy={currentY}
    r="2"
    class="fill-neutral-8 @dark:fill-neutral-3"
  />
</svg>
<div class="fixed w-screen h-screen">
  <div class="@dark:text-neutral-3 font-bold text-center text-xl mt-5">
    amplitude={(Math.hypot(currentX - 150, currentY - 150) / 150).toPrecision(
      3
    )}
  </div>
  <div class="flex justify-center gap-10 mt-5">
    <div>
      <div class="@dark:text-neutral-3 font-bold text-center text-xl">
        phasors = {phasors}
      </div>
      <input type="range" bind:value={phasors} min="1" max="200" />
    </div>
    <div>
      <div class="@dark:text-neutral-3 font-bold text-center text-xl">
        total angle = {totalAngle.toPrecision(3)}
      </div>
      <input
        type="range"
        bind:value={totalAngle}
        max={6 * Math.PI}
        step={Math.PI / 20}
      />
    </div>
  </div>
</div>
