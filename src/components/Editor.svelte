<script>
  import ObjectMenu from "./ObjectMenu.svelte";
  import ObjectBlock from "./ObjectBlock.svelte";
  let editor;
  let blockList = [];
  const addBlock = (posX, posY) => {
    blockList = blockList.concat({ posX, posY });
    console.log(blockList)
  };
</script>

<div
  class="editor"
  bind:this={editor}
  on:drop={(event) => {
    addBlock(event.layerX, event.layerY);
  }}
  on:dragover|preventDefault
>
  {#each blockList as props}
    <ObjectBlock props={props} />
  {/each}
</div>
<ObjectMenu />

<style>
  .editor {
    width: 100%;
    height: 100%;
  }
</style>
