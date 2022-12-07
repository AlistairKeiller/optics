<script>
  import "uno.css";
  import "@unocss/reset/tailwind.css";
  let numberOfPhasors = 100,
    totalAngle = Math.PI,
    path,
    currentX,
    currentY;
  var i;
  $: for (
    currentX = 150, currentY = 150, path = `M${currentX} ${currentY} `, i = 0;
    i < numberOfPhasors;
    i++
  ) {
    currentX +=
      (150 / numberOfPhasors) * Math.cos((totalAngle * i) / numberOfPhasors);
    currentY +=
      (150 / numberOfPhasors) * Math.sin((totalAngle * i) / numberOfPhasors);
    path += `L${currentX} ${currentY} `;
  }
</script>

<svg class="fixed w-screen h-screen" viewBox="0 0 300 300">
  <path stroke="#0284c7" stroke-width="2" fill="none" d={path} />
  <circle cx={currentX} cy={currentY} fill="#262626" r="2" />
</svg>
<div class="fixed w-screen h-screen">
  <div class="text-center text-xl mt-5">
    amplitude={(Math.hypot(currentX - 150, currentY - 150) / 150).toPrecision(
      3
    )}
  </div>
  <div class="flex justify-center gap-10 mt-5">
    <div>
      <div class="text-center text-xl">
        number of phasors = {numberOfPhasors}
      </div>
      <input type="range" bind:value={numberOfPhasors} min="1" max="200" />
    </div>
    <div>
      <div class="text-center text-xl">
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
