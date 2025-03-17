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

<style scoped>
.anonymization-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 20px; 
  max-width: 900px; 
  width: 100%;
  margin: 0 auto;
  margin-top: 60px;
  padding-right: 300px;
}

.upload-steps {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.step {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 18px;
  color: #333;
}

.bold-text {
  font-weight: bold;
}

.step-icon {
  width: 40px;
  height: 40px;
  margin-bottom: 5px;
}

.arrow-icon {
  width: 24px;
  height: 24px;
}

.upload-box {
  background: white;
  border-radius: 10px;
  padding: 40px; 
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 700px; 
  width: 100%;
}

.drop-zone {
  border: 2px dashed #ccc;
  border-radius: 8px;
  padding: 30px;
  text-align: center;
  margin-top: 10px;
  font-weight: 500;
  font-size: 22px;
  font-family: 'Montserrat', sans-serif;
}

.drop-zone.drag-over {
  background-color: #f0f0f0;
}


.or-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 15px 0;
  font-family: 'Montserrat', sans-serif;
}

.or-text {
  color: gray;
  position: relative;
  z-index: 7; 
  margin-bottom: 5px;
  padding: 0 10px; 
}

.browse-button {
  background: #3865F2;
  color: white;
  border: none;
  padding: 10px 20px;
  font-size: 20px;
  border-radius: 25px;
  cursor: pointer;
  margin-top: 5px;
}

.browse-button:hover {
  background: #2f55d4;
}
</style>

