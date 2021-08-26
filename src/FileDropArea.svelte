<script>
import { createEventDispatcher } from "svelte"

let dropArea = {}
let highlighted = false

const dispatch = createEventDispatcher()

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
  console.log(formData.get('file'))
}

</script>

<style>
#drop-area {
  border: 2px dashed #ccc;
  border-radius: 20px;
  width: 480px;
  font-family: sans-serif;
  margin: 100px auto;
  padding: 20px;
}
#drop-area.highlighted {
  border-color: purple;
}
p {
  margin-top: 0;
}
.my-form {
  margin-bottom: 10px;
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
.button {
  display: inline-block;
  padding: 10px;
  background: #ccc;
  cursor: pointer;
  border-radius: 5px;
  border: 1px solid #ccc;
}
.button:hover {
  background: #ddd;
}
#fileElem {
  display: none;
}

</style>

<div id="drop-area" bind:this={dropArea} class:highlighted
 on:dragenter|preventDefault|stopPropagation={highlight}
 on:dragleave|preventDefault|stopPropagation={unhighlight}
 on:dragover|preventDefault|stopPropagation={highlight}
 on:drop|preventDefault|stopPropagation={evt => handleDrop(evt) && unhighlight(evt)}>
  <form class="my-form">
    <p>Upload multiple files with the file dialog or by dragging and dropping images onto the dashed region</p>
    <input type="file" id="fileElem" multiple accept="image/*" onchange="handleFiles(this.files)">
    <label class="button" for="fileElem">Select some files</label>
  </form>
</div>
