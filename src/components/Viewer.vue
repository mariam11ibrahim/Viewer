<script>
export default {
  data() {
    return {
      reader: new FileReader(),
      files: [],
      srcs: [],
      isDialogOPen: false,
    };
  },
  methods: {
    closeDialog() {
      console.log("close");
      this.isDialogOPen = false;
      this.files = [];
      this.reader.abort();
    },
    handleFileUpload(event) {
      this.isDialogOPen = true;
      this.files = event.target.files;
      this.previewVideo();
    },

    previewVideo() {
      let files = this.files;
      let reader = this.reader;
      this.reader.readAsDataURL(this.files[0]);
      this.reader.addEventListener("load", function () {
        for (let i = 0; i < files.length; i++) {
          let video = document.getElementById("video-preview" + i);
          video.src = reader.result;
        }
      });
    },
  },
};
</script>
<template>
  <div class="backdrop" v-if="isDialogOPen"></div>
  <section>
    <div class="container">
      <div>
        <h2>Video File Preview</h2>
        <hr />
        <label
          >Video File
          <input
            type="file"
            accept="video/*"
            multiple
            @change="handleFileUpload($event)"
          />
        </label>
        <br />

        <dialog v-show="files.length != 0" class="base-dialog" open>
          <video
            v-for="(file, index) of files"
            :key="file.name"
            :id="'video-preview' + index"
            controls
            v-show="files.length != 0"
          />
          <button @click="closeDialog">Close</button>
        </dialog>
        <br />
      </div>
    </div>
  </section>
</template>

<style scoped>
section {
  height: 100%;
  position: relative;
}
.backdrop {
  background: rgba(0, 0, 0, 0.5);
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  z-index: 10;
}
.container {
  margin: 50px;
  border: 2px dashed #2e2e2e;
  border-radius: 5px;
}
video {
  width: 400px;
  height: 400px;
  padding: 5px;
  border: 1px solid gray;
  border-radius: 5px;
}
label,
button {
  position: relative;
  display: inline-block;
  background: #2e2e2e;
  color: #ffff;
  border-radius: 100px;
  cursor: pointer;
  text-align: center;
  padding: 10px 20px;
  border: 0;
  z-index: 0;
}
button {
  background: #f44336;
  position: absolute;
  top: 10px;
  right: 30px;
}
input {
  position: absolute;
  display: none;
}
.base-dialog {
  position: absolute;
  overflow-y: scroll;
  border-radius: 5px;
  top: 10px;
  left: 50%;
  transform: translateX(-50%);
  padding: 40px;

  box-shadow: rgba(0, 0, 0, 0.05) 0px 1px 2px 0px;
  border: 1px solid #2e2e2e;
  width: 70%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  z-index: 20;
  height: 70%;
}
</style>
