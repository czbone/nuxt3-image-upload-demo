<template>
  <vue-dropzone
    ref="myVueDropzone"
    id="dropzone"
    :options="dropzoneOptions"
    @vdropzone-error="uploadError"
  />
</template>
<script>
import vueDropzone from 'vue2-dropzone-vue3'

export default {
  components: {
    vueDropzone,
  },
  data () {
    return {
      dropzoneOptions: {
        url: '/api/file',
        thumbnailWidth: 150,
        maxFilesize: 0.5,
        headers: { "My-Awesome-Header": "header value" },
        //headers: { 'X-CSRF-TOKEN': this.token }
        //headers: { "X-CSRF-TOKEN": document.head.querySelector("[name=csrf-token]").content }
        dictFileTooBig: 'ファイルサイズの上限は {{maxFilesize}} MB です\n(size: {{filesize}} MB)',
        dictDefaultMessage: 'ファイルをここにドロップ、またはマウスクリックでアップロード',
      },
    }
  },
  methods:{
    uploadError(file, message, xhr){
      if (message instanceof Object){   // サーバ側でエラーの場合はObjectが来る
        file.previewElement.querySelectorAll('.dz-error-message span')[0].textContent = message.message
      }
    }
  }
}
</script>
<style>
/* アイコンの表示位置を修正 */
.vue-dropzone > .dz-preview .dz-success-mark, .vue-dropzone > .dz-preview .dz-error-mark {
  width: 54px;
  left: 50%;
  margin-left: -27px;
}
.vue-dropzone > .dz-preview .dz-success-mark {
  background-color: green;
}
.vue-dropzone > .dz-preview .dz-error-mark {
  background-color: red;
}
</style>