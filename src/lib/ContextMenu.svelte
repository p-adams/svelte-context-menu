<script lang="ts">
  import { onMount } from "svelte";

  let menu: HTMLDivElement | null = null;
  let widthHeight: { width?: number; height?: number } | null = null;
  onMount(() => {
    widthHeight = {
      width: menu?.children[0].clientWidth,
      height: menu?.children[0].clientHeight,
    };
  });
</script>

<div
  bind:this={menu}
  class="context-menu-wrapper"
  style:width={`${widthHeight?.width && widthHeight.width + 50}px`}
  style:height={`${widthHeight?.height && widthHeight.height + 50}px`}
>
  <slot />
</div>

<style>
  .context-menu-wrapper {
    outline: 1px solid red;

    display: flex;
    justify-content: center;

    align-items: center;
  }
</style>
