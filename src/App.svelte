<script lang="ts">
  import ContextMenu from "./lib/ContextMenu.svelte";
  let showMenuDialog = false;
  let selectedMenuItem: string | null = null;
  function dialogClick(
    e: MouseEvent & {
      currentTarget: EventTarget & HTMLUListElement;
    }
  ) {
    const target = e.target as HTMLElement;
    selectedMenuItem = target?.textContent;
    showMenuDialog = false;
  }
</script>

<main>
  <h1>Svelte Context Menu</h1>

  <div class="card">
    <ContextMenu
      {showMenuDialog}
      on:closeDialog={() => (
        (showMenuDialog = false), (selectedMenuItem = null)
      )}
      on:openDialog={() => (showMenuDialog = true)}
    >
      <div class="demo-card" slot="content">
        <h1>Foo Bar Baz</h1>
        <div>foo bar baz quux</div>
      </div>
      <div slot="dialog-content">
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
        <ul on:click={(e) => dialogClick(e)}>
          <li>A</li>
          <li>B</li>
          <li>C</li>
        </ul>
      </div>
    </ContextMenu>
  </div>

  <p>
    Check out <a
      href="https://github.com/sveltejs/kit#readme"
      target="_blank"
      rel="noreferrer">Guide</a
    >
  </p>
</main>

<style>
  .demo-card {
    width: 275px;
    height: 350px;
    outline: 1px solid black;
    background-color: white;
    cursor: pointer;
  }
</style>
