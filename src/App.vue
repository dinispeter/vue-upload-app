<template>
  <div id="app">
    <h1>Vue upload súborov</h1>
    <br>
    <FilePond
    name="image"
    ref="pond"
    allowMultiple="true"
    class-name="my-pond"
    label-idle="Drop files here..."
    v:bind-files="myFiles"
    :allowImagePreview="true"
    :allowImageCrop="true"
    labelFileProcessingComplete="Upload bol dokončený"
    labelFileProcessing="Súbor sa uploaduje"
    :server="{process}"

    />


  </div>
</template>

<script>
  import vueFilePond from 'vue-filepond';
  import FilePondPluginImagePreview from 'filepond-plugin-image-preview';
  import FilePondPluginFileValidateType from 'filepond-plugin-file-validate-type/dist/filepond-plugin-file-validate-type.esm.js';
  import FilePondPluginImageCrop from 'filepond-plugin-image-crop';
  import FilePondPluginGetFile from 'filepond-plugin-get-file';
  import 'filepond/dist/filepond.min.css';
  import "filepond-plugin-get-file/dist/filepond-plugin-get-file.css";
  import 'filepond-plugin-image-preview/dist/filepond-plugin-image-preview.min.css';

export default {
    name: 'app',
    components: {
      FilePond: vueFilePond(FilePondPluginGetFile, FilePondPluginImagePreview, FilePondPluginImageCrop, FilePondPluginFileValidateType )
    },

    data: function() {
      return {
        myFiles: [""],

      }
    },

    methods: {
      process(fieldName, file, metadata, load) {
        load(file);
      },
      handleFilePondInit() {
        this.$refs.pond.getFiles();
      },
    }
  }
</script>


<style>
  h1 {
    text-align: center;
  }
</style>
