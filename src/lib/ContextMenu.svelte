<script lang="ts">
  import { createEventDispatcher, onMount } from "svelte";
  const dispatch = createEventDispatcher();

  let menu: HTMLDivElement | null = null;
  let widthHeight: { width?: number; height?: number } | null = null;
  let showMenuButton: boolean = false;
  export let showMenuDialog: boolean = false;
  export let dialogContentItems: any[] = [];

  onMount(() => {
    widthHeight = {
      width: menu?.children[0].clientWidth,
      height: menu?.children[0].clientHeight,
    };
  });

  function dialogClick(
    e: MouseEvent & {
      currentTarget: EventTarget & HTMLUListElement;
    }
  ) {
    const target = e.target as HTMLElement;
    dispatch("selectMenuItem", { item: target?.textContent });
  }
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
  class="context-menu-outer"
  on:mouseenter={() => (showMenuButton = true)}
  on:mouseleave={() => (showMenuButton = false)}
>
  {#if showMenuButton}
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <slot name="menu-btn">
      <div
        class="menu-btn"
        on:click={() => dispatch("openDialog")}
        on:keypress={() => dispatch("openDialog")}
      >
        ...
      </div>
    </slot>
  {/if}

  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
  <dialog open={showMenuDialog}>
    <slot name="dialog-content">
      <ul class="dialog-content-items" on:click={(e) => dialogClick(e)}>
        {#each dialogContentItems as item}
          <li class="dialog-content-item">{item}</li>
        {/each}
      </ul>
    </slot>
    <button on:click={() => dispatch("closeDialog")}>X</button>
  </dialog>
  <div
    bind:this={menu}
    class="context-menu-inner"
    style:width={`${widthHeight?.width && widthHeight.width + 50}px`}
    style:height={`${widthHeight?.height && widthHeight.height + 50}px`}
  >
    <slot name="content" />
  </div>
</div>

<style>
  .context-menu-outer {
    position: relative;
  }
  .context-menu-outer:hover {
    background-color: lightgray;
    border-radius: 2%;
  }
  .menu-btn {
    position: absolute;
    font-size: 42px;
    right: 10px;
    top: -32px;
    cursor: pointer;
  }
  .context-menu-inner {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .dialog-content-item {
    cursor: pointer;
  }
  .dialog-content-item:hover {
    background-color: lightgray;
  }
</style>
