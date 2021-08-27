<script>
import { createEventDispatcher } from "svelte"

export let raised = false
export let outlined = false

let fileInput = {}

let highlighted = false

const dispatch = createEventDispatcher()

function highlight() {
  highlighted = true
}

function unhighlight() {
  highlighted = false
}

function handleDrop(e) {
  unhighlight()

  let dt = e.dataTransfer
  let files = dt.files

  handleFiles(files)
}

function handleFiles(files) {
  ([...files]).forEach(uploadFile)
}

function uploadFile(file) {
  const formData = new FormData()

  formData.append('file', file)

  dispatch('upload', formData)
}

</script>

<style>
#drop-area {
  border: 2px dashed #ccc;
  border-radius: 20px;
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
form {
  gap: 10px;
  align-items: center;
  justify-items: center;
}

</style>

<div id="drop-area" class="p-20px {$$props.class}" class:highlighted
 on:dragenter|preventDefault|stopPropagation={highlight}
 on:dragleave|preventDefault|stopPropagation={unhighlight}
 on:dragover|preventDefault|stopPropagation={highlight}
 on:drop|preventDefault|stopPropagation={handleDrop}>
  <form class="flex mb-10px">
    <input bind:this={fileInput} type="file" id="fileElem" multiple accept="image/*" on:change={() => handleFiles(fileInput.files)}>
    <label class="mdc-button" for="fileElem" class:mdc-button--outlined={outlined} class:mdc-button--raised={raised}>Choose files</label>
    <div>or drop files here</div>
    <i class="material-icons mdc-theme--primary" id="upload-icon">cloud_upload</i>
  </form>
</div>
