<script>
  import ObjectMenu from "./components/ObjectMenu.svelte";
</script>

<div
class="editor"
  on:drop={(event) => {
    console.log(event);
  }}
  on:dragover|preventDefault
>
</div>
<ObjectMenu />
<style>
    .editor{
        width:100%;
        height: 100%;
    }
</style>
