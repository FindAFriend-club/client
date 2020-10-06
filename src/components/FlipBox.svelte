<script lang="typescript">
  export let isFlipped;

  let frontHeight: number;
  let backHeight: number;

  $: flipBoxHeight = Math.max(backHeight, frontHeight)
</script>

<style lang="sass">
    .flip-box
        perspective: 1000px

        &.isFlipped
            .flip-box-inner
                transform: rotateY(180deg)

        .flip-box-inner
            display: flex
            transition: transform 0.8s, height 0.8s
            transform-style: preserve-3d
            flex-flow: row nowrap

            .front, 
            .back
                width: 100%
                -webkit-backface-visibility: hidden
                backface-visibility: hidden
                flex: none

            .back
                transform: rotateY(180deg) translateX(100%)
</style>

<div class="flip-box" class:isFlipped>
  <div class="flip-box-inner" style={`height: ${flipBoxHeight}px`}>
    <div bind:offsetHeight={frontHeight} class="front">
      <slot name="front" />
    </div>
    <div bind:offsetHeight={backHeight} class="back">
      <slot name="back" />
    </div>
  </div>
</div>
