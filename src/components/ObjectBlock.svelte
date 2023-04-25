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
  @import url('https://fonts.cdnfonts.com/css/google-sans');
  .object-block {
    background-color: rgba(255, 229, 127, 0.731);
    border-radius: 20px;
    font-size: 11pt;
    font-family: 'Product Sans Medium';
    min-width: clamp(200px, 15vh, 15vh);
    color: #000;
    min-width: clamp(200px, 15vw, 15vw);
    position: absolute;
    box-shadow: 0px 0px 3px 3px rgba(0, 23, 14, 0.314);
  }
  #object-block-sel {
    cursor: grab;
    background-color: rgba(224, 224, 224, 0.597);
    border: solid 1px rgb(0, 0, 0);
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
  }
  .object-place {
    min-width: 150px;
    min-height: 150px;
    background-color: rgba(168, 243, 255, 0.427);
    border-radius: 20px;
    transition: 0.1s;
  }
  .object-place:hover {
    box-shadow: 0px 0px 1px 1px rgb(255, 221, 0);
    background-color: rgba(197, 250, 255, 0.847);
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
    color: #000;
    padding-left: 20px;
    padding-right: 20px;
    padding-bottom: 20px;
  }
</style>
