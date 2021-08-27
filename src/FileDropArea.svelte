<script>
import { MDCRipple } from '@material/ripple'
import { createEventDispatcher, onMount } from "svelte"

export let raised = false
export let outlined = false

let dropArea = {}
let button = {}
let highlighted = false

const dispatch = createEventDispatcher()

onMount(() => {
  const ripple = new MDCRipple(button)
  return () => ripple.destroy()
})

function highlight() {
  highlighted = true
}

function unhighlight() {
  highlighted = false
}

function handleDrop(e) {
  let dt = e.dataTransfer
  let files = dt.files

  handleFiles(files)
}

function handleFiles(files) {
  ([...files]).forEach(uploadFile)
}

function uploadFile(file) {
  let formData = new FormData()

  formData.append('file', file)

  dispatch('upload', formData)
}

</script>

<style>
#drop-area {
  border: 2px dashed #ccc;
  border-radius: 20px;
  width: 480px;
  font-family: sans-serif;
  margin: 100px auto;
}
#drop-area.highlighted {
  border-color: var(--mdc-theme-primary);
}
#gallery {
  margin-top: 10px;
}
#gallery img {
  width: 150px;
  margin-bottom: 10px;
  margin-right: 10px;
  vertical-align: middle;
}
#fileElem {
  display: none;
}

</style>

<div id="drop-area" bind:this={dropArea} class="p-20px {$$props.class}" class:highlighted
 on:dragenter|preventDefault|stopPropagation={highlight}
 on:dragleave|preventDefault|stopPropagation={unhighlight}
 on:dragover|preventDefault|stopPropagation={highlight}
 on:drop|preventDefault|stopPropagation={evt => handleDrop(evt) && unhighlight(evt)}>
  <form class="mb-10px">
    <p class="mt-0">Upload multiple files with the file dialog or by dragging and dropping images onto the dashed region</p>
    <input type="file" id="fileElem" multiple accept="image/*" onchange="handleFiles(this.files)">
    <label class="mdc-button" for="fileElem" class:mdc-button--outlined={outlined} class:mdc-button--raised={raised} bind:this={button}>Select some files</label>
  </form>
</div>
