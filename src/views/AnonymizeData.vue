<template>
  <BaseLayout>
    <div class="anonymization-content">
      <div class="upload-steps">
        <div class="step">
          <img src="../assets/upload.svg" alt="File Upload" class="step-icon" />
          <span :class="{ 'bold-text': file }">File upload</span>
        </div>
        <img src="../assets/arrow.svg" alt="Arrow" class="arrow-icon" />
        <div class="step">
          <img src="../assets/attach.svg" alt="Add Files" class="step-icon" />
          <span :class="{ 'bold-text': file }">Add files</span>
        </div>
        <img src="../assets/arrow.svg" alt="Arrow" class="arrow-icon" />
        <div class="step">
          <img src="../assets/share.svg" alt="Share Files" class="step-icon" />
          <span>Share files</span>
        </div>
      </div>

      <div class="upload-box">
        <h2>Add your file to get started</h2>
        <div 
          class="drop-zone" 
          @dragover.prevent="handleDragOver" 
          @dragleave.prevent="handleDragLeave" 
          @drop.prevent="handleDrop"
          :class="{ 'drag-over': isDragging }"
        >
        <p v-if="!file">Drag or drop file here</p>
          <p v-else>{{ file.name }}</p>
          <div class="or-container" v-if="!file">
            <span class="or-text">or</span>
          </div>
          <label for="fileInput" class="browse-button">Browse your file</label>
          <input type="file" id="fileInput" @change="handleFileChange" style="display: none;" />
        </div>
      </div>
    </div>
  </BaseLayout>
</template>

<script>
import BaseLayout from "../layouts/BaseLayout.vue";

export default {
  name: "AnonymizeData",
  components: {
    BaseLayout,
  },
  data() {
    return {
      file: null,
      processedContent: "",
      fileType: "",
      isDragging: false,
    };
  },
  methods: {
    handleFileChange(event) {
      this.file = event.target.files[0];
    },
    handleDragOver(event) {
      this.isDragging = true;
    },
    handleDragLeave(event) {
      this.isDragging = false;
    },
    handleDrop(event) {
      this.isDragging = false;
      if (event.dataTransfer.files.length) {
        this.file = event.dataTransfer.files[0];
      }
    },
    async handleSubmit() {
      if (!this.file) {
        alert("Please upload a file.");
        return;
      }

      const formData = new FormData();
      formData.append("file", this.file);
      formData.append("processType", "anonymize");

      try {
        const response = await fetch("http://localhost:8080/api/files/upload", {
          method: "POST",
          body: formData,
        });

        const result = await response.text();
        this.processedContent = result;
        alert("Processing successful!");
      } catch (error) {
        console.error("Error uploading file:", error);
        alert("Error uploading file: " + error.message);
      }
    },
  },
};
</script>

<style lang="scss">
@use '../styles/variables' as v;
@use '../styles/mixins' as m;
@use '../styles/utilities' as u;
@use '../styles/components' as c;

.anonymization-content {
  @include m.flex-column;
  @include m.container;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: v.$spacing-lg;
  margin-top: 60px;

  @include m.mobile {
    margin-top: v.$spacing-lg;
    padding: v.$spacing-md;
  }
}

.upload-steps {
  @include m.flex-center;
  gap: v.$spacing-lg;
  margin-bottom: v.$spacing-xl;
  flex-wrap: wrap;

  @include m.mobile {
    gap: v.$spacing-md;
    margin-bottom: v.$spacing-lg;
  }
}

.step {
  @include m.flex-column;
  align-items: center;
  font-size: v.$font-size-md;
  color: v.$text-color;

  @include m.mobile {
    font-size: v.$font-size-sm;
    min-width: 100px;
  }
}

.bold-text {
  font-weight: bold;
}

.step-icon {
  width: 40px;
  height: 40px;
  margin-bottom: v.$spacing-xs;

  @include m.mobile {
    width: 30px;
    height: 30px;
  }
}

.arrow-icon {
  width: 24px;
  height: 24px;

  @include m.mobile {
    width: 16px;
    height: 16px;
  }

  @include m.tablet {
    transform: rotate(90deg);
  }
}

.upload-box {
  background: v.$white;
  border-radius: 10px;
  padding: v.$spacing-xl;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 700px;

  @include m.mobile {
    padding: v.$spacing-lg;
  }

  h2 {
    @include m.mobile {
      font-size: v.$font-size-lg;
    }
  }
}

.drop-zone {
  border: 2px dashed v.$gray;
  border-radius: 8px;
  padding: v.$spacing-xl;
  text-align: center;
  margin-top: v.$spacing-sm;
  font-weight: 500;
  font-size: v.$font-size-lg;
  font-family: v.$primary-font;

  @include m.mobile {
    padding: v.$spacing-lg;
    font-size: v.$font-size-md;
  }

  &.drag-over {
    background-color: v.$background-color;
  }
}

.or-container {
  @include m.flex-center;
  margin: v.$spacing-md 0;
  font-family: v.$primary-font;
}

.or-text {
  color: v.$gray;
  position: relative;
  z-index: 7;
  margin-bottom: v.$spacing-xs;
  padding: 0 v.$spacing-sm;
}

.browse-button {
  @extend .button;
  margin-top: v.$spacing-xs;

  @include m.mobile {
    font-size: v.$font-size-sm;
    padding: v.$spacing-xs v.$spacing-md;
  }
}
</style>

