<template>
  <div class="upload-panel">
    <div
      class="tittle"
      v-if="uploadingFiles.length"
      @click="isShowUploadingContent = !isShowUploadingContent"
    >
      Uploading ({{ rawUploadingFiles.length }})
    </div>
    <div
      class="list-upload-file"
      v-if="uploadingFiles.length && isShowUploadingContent"
    >
      <div
        class="file"
        v-for="(upload, index) in uploadingFiles"
        :key="'upload' + index"
      >
        <div>
          <div class="file-name">
            {{ upload.file.name }}
          </div>
          <div class="progress">
            {{ formatBytes(upload.loaded) }} /
            {{ formatBytes(upload.file.size) }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { formatBytes } from "@/utils/files";
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters(["uploads"]),
    rawUploadingFiles() {
      return (Object.values(this.uploads) || []).filter(
        (upload) => upload.file
      );
    },
    uploadingFiles() {
      return this.rawUploadingFiles.slice(0, 3);
    },
  },
  methods: {
    formatBytes,
  },
  data() {
    return {
      isShowUploadingContent: true,
    };
  },
};
</script>
