<script lang="ts">
  import ContextMenu from "./lib/ContextMenu.svelte";
</script>

<main>
  <h1>Svelte Context Menu</h1>

  <div class="card">
    <ContextMenu>
      <div class="card">
        <h1>Foo Bar Baz</h1>
        <div>foo bar baz quux</div>
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
  .card {
    width: 275px;
    height: 350px;
  }
</style>
