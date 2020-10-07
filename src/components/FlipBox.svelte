<script lang="typescript">
  import { afterUpdate, onMount } from "svelte";

  export let isFlipped;
</script>

<style lang="sass">
    .flip-box
        perspective: 1000px

        &.isFlipped
            .flip-box-inner
                transform: rotateY(-180deg)

        .flip-box-inner
            display: grid
            transition: transform 0.8s, height 0.8s
            transform-style: preserve-3d
            grid-template-rows: 1fr

            .front,
            .back
                display: flex
                -webkit-backface-visibility: hidden
                backface-visibility: hidden
                grid-row-start: 1
                grid-column-start: 1
                align-items: center
                justify-content: center

            .back
                transform: rotateY(-180deg)
</style>

<div class="flip-box" class:isFlipped>
  <div class="flip-box-inner">
    <div class="front">
      <slot name="front" />
    </div>
    <div class="back">
      <slot name="back" />
    </div>
  </div>
</div>
