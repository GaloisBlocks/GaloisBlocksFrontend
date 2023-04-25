<script>
  import {dragging} from '../js/stores';
  let draggedElement;
  let self;
  dragging.subscribe((value)=>{draggedElement = value})
  export var props;
  let left = props.posX;
  let top = props.posY;

  function handleDragStart(event) {
    event.preventDefault()
    dragging.set(self);
    if( draggedElement.style.position == "static"){
      draggedElement.style.position = "fixed"
      console.log(event)
      left = event.clientX
      top = event.clientY
    }
    console.log(self)
    draggedElement.style.pointerEvents = "none";
    window.addEventListener("mousemove", handleMouseMove);
    window.addEventListener("mouseup",()=>{ event.target.dispatchEvent(new Event("dragend"))});
  }
  const dropped = (event)=>{
    console.log({target: event.target})
    event.target.appendChild(draggedElement)
    draggedElement.style.position = "static"
  }
  function handleDragOver(event) {
    event.target.addEventListener('mouseup',dropped)
  }
  function handleDragLeave(event){
    event.target.removeEventListener('mouseup',dropped)
  }
  function handleMouseMove(event) {
      left += event.movementX;
      top += event.movementY;
      if (left < 0) left = 0;
      if (top < 0) top = 0;
  }

  function handleDragEnd(event) {
    window.removeEventListener("mousemove", handleMouseMove);
    draggedElement.style.pointerEvents = "auto";
    console.log(draggedElement)
    dragging.set(null);
    console.log(draggedElement)
  }
</script>

<div
  class="object-block"
  bind:this={self}
  style="top:{top}px; left:{left}px;"
>
  <div draggable={true} on:dragstart={handleDragStart} on:dragend={handleDragEnd} id="object-block-sel">NFT Collection</div>
  <div class="content">
    <div class="object-place-name">Media:</div>
    <div
      class="object-place"
      on:focus={()=>{}}
      on:mouseover={handleDragOver}
      on:mouseleave={handleDragLeave}
    />
  </div>
</div>

<style>
  .object-block {
    border: dashed 1px rgb(0, 0, 0);
    background-color: rgba(0, 81, 49, 0.316);
    border-radius: 5px;
    font-size: 10pt;
    font-family: Verdana;
    min-width: clamp(200px, 15vh, 15vh);
    color: #000;
    min-width: clamp(200px, 15vw, 15vw);
    position: absolute;
  }
  #object-block-sel {
    background-color: rgb(123, 123, 123);
    border: solid 1px rgb(0, 0, 0);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
  .object-place {
    min-width: 150px;
    min-height: 150px;
    background-color: rgba(168, 243, 255, 0.427);
    border-radius: 5px;
    transition: 0.2s;
  }
  .object-place:hover {
    box-shadow: 0px 0px 1px 1px rgb(32, 181, 255);
    border: 0.5px dashed rgb(32, 181, 255);
  }
  .object-place-name {
    width: 80%;
    text-align: left;
  }
  .content {
    padding-top: 5px;
    display: flex;
    flex-direction: column;
    align-items: center;
    color: #fff;
    padding-left: 20px;
    padding-right: 20px;
    padding-bottom: 20px;
  }
</style>
