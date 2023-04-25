<script>
  import ObjectMenu from "./ObjectMenu.svelte";
  import ObjectBlock from "./ObjectBlock.svelte";
  import {dragging} from '../js/stores';
  let draggedElement;
  dragging.subscribe((value)=>{draggedElement = value})
  const dropped = (event)=>{
    event.target.appendChild(draggedElement)
  }
  function handleDragOver(event) {
    event.target.addEventListener('mouseup',dropped)
  }
  function handleDragLeave(event){
    event.target.removeEventListener('mouseup',dropped)
  }
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
  on:focus={()=>{}}
  on:mouseover={handleDragOver}
  on:mouseleave={handleDragLeave}
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
