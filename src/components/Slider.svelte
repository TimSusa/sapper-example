<script>
  let circleLeft = 0;
  let prevLeft = 0;
  let circleTop = 0;
  let prevTop = 0;
  let hasCapture = false;
  let dragging = false;

  function onDown(event) {
    event.target.setPointerCapture(event.pointerId);

    // We store the initial coordinates to be able to calculate the changes
    // later on.
    dragging = true;
    prevLeft = event.pageX;
    prevTop = event.pageY;
  }

  function onMove(event) {
    if (!dragging) return;
    const dx = event.pageX - prevLeft;
    const dy = event.pageY - prevTop;

    //circleLeft = circleLeft + dx;
    circleTop = circleTop + dy;
    prevLeft = event.pageX;
    prevTop = event.pageY;
  }

  function cancelDragging() {
    dragging = false;
  }
  function setHasCapture(hasC) {
    hasCapture = hasC;
  }
</script>

<style>
  .slider {
    height: 150px;
    width: 60px;
    background: grey;
  }
  .circle {
    width: 60px;
    height: 30px;
    border-radius: 3px;
    position: absolute;
    touch-action: none;
    will-change: transform;
  }
</style>

<div class="slider">
  <div
    class="circle"
    style="transform: translate({circleLeft}px, {circleTop}px); background: {hasCapture ? 'blue' : 'green'}
    "
    on:pointerdown={onDown}
    on:pointermove={onMove}
    on:pointerup={cancelDragging}
    on:pointercancel={cancelDragging}
    on:gotpointercapture={() => setHasCapture(true)}
    on:lostpointercapture={() => setHasCapture(false)} />
</div>
