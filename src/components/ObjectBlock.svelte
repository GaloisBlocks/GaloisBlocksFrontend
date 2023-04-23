<script>
  import "iconify-icon";
  export var props = {
    posX: 100,
    posY: 100,
  };
  let moving = false;
  function dragMe(node) {
    let left = props.posX;
    let top = props.posY;

    node.style.position = "absolute";
    node.style.top = `${top}px`;
    node.style.left = `${left}px`;
    node.style.cursor = "move";
    node.style.userSelect = "none";

    window.addEventListener("mousemove", (e) => {
      if (moving) {
        left += e.movementX;
        top += e.movementY;
        if (left < 0) left = 0;
        if (top < 0) top = 0;
        node.style.top = `${top}px`;
        node.style.left = `${left}px`;
      }
    });

    window.addEventListener("mouseup", () => {
      moving = false;
    });
  }
</script>

<div class="object-block" use:dragMe>
  <div on:mousedown={() => (moving = true)} id="object-block-sel">Hola</div>
</div>

<style>
  .object-block {
    border: dashed 1px rgb(0, 0, 0);
    background-color: rgb(255, 0, 0);
    border-radius: 5px;
    font-size: 10pt;
    font-family: Verdana;
    height: 100px;
    color: #000;
    width: clamp(150px, 10vw, 10vw);
  }
  #object-block-sel {
    background-color: rgb(123, 123, 123);
    border: solid 1px rgb(0, 0, 0);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
</style>
