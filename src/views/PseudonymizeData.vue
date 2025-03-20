<template>
  <BaseLayout>
    <div class="pseudonymize">
      <div class="header">
        <h1>Pseudonymize Data</h1>
        <p class="subtitle">Create reversible data masks while maintaining data utility</p>
      </div>

      <div class="upload-section">
        <div class="upload-card">
          <img src="../assets/upload.svg" alt="Upload" class="upload-icon" />
          <h2>Upload Your Data</h2>
          <p>Drag and drop your files here or click to browse</p>
          <label for="file-upload-pseudo" class="sr-only">Choose files to pseudonymize</label>
          <input 
            type="file" 
            id="file-upload-pseudo"
            class="file-input" 
            @change="handleFileUpload" 
            multiple
            aria-label="Choose files to pseudonymize"
            title="Choose files to pseudonymize"
          />
          <button class="upload-btn" @click="triggerFileInput">
            <span class="icon">+</span>
            Select Files
          </button>
        </div>

        <div class="info-card">
          <h3>About Pseudonymization</h3>
          <p>Pseudonymization replaces sensitive data with reversible identifiers, allowing for:</p>
          <ul>
            <li>Data analysis while protecting privacy</li>
            <li>Reversible data transformation</li>
            <li>Compliance with data protection regulations</li>
            <li>Secure data sharing between organizations</li>
          </ul>
          <div class="supported-formats">
            <h4>Supported Formats</h4>
            <div class="format-tags">
              <span class="tag">CSV</span>
              <span class="tag">JSON</span>
              <span class="tag">XML</span>
              <span class="tag">Excel</span>
            </div>
          </div>
        </div>
      </div>

      <div v-if="uploadedFiles.length > 0" class="files-section">
        <h2>Uploaded Files</h2>
        <div class="files-list">
          <div v-for="file in uploadedFiles" :key="file.name" class="file-item">
            <div class="file-info">
              <span class="file-name">{{ file.name }}</span>
              <span class="file-size">{{ formatFileSize(file.size) }}</span>
            </div>
            <button class="remove-btn" @click="removeFile(file)">Remove</button>
          </div>
        </div>
        <div class="actions">
          <button class="process-btn" @click="processPseudonymization">
            Start Pseudonymization
          </button>
        </div>
      </div>
    </div>
  </BaseLayout>
</template>

<script>
import BaseLayout from '../layouts/BaseLayout.vue';

export default {
  name: 'PseudonymizeData',
  components: {
    BaseLayout
  },
  data() {
    return {
      uploadedFiles: []
    }
  },
  methods: {
    triggerFileInput() {
      document.querySelector('.file-input').click();
    },
    handleFileUpload(event) {
      const files = Array.from(event.target.files);
      this.uploadedFiles.push(...files);
    },
    removeFile(file) {
      const index = this.uploadedFiles.indexOf(file);
      if (index > -1) {
        this.uploadedFiles.splice(index, 1);
      }
    },
    formatFileSize(bytes) {
      if (bytes === 0) return '0 Bytes';
      const k = 1024;
      const sizes = ['Bytes', 'KB', 'MB', 'GB'];
      const i = Math.floor(Math.log(bytes) / Math.log(k));
      return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
    },
    processPseudonymization() {
      console.log('Starting pseudonymization for files:', this.uploadedFiles);
    }
  }
}
</script>

<style lang="scss" scoped>
.pseudonymize {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.header {
  text-align: center;
  margin-bottom: 40px;

  h1 {
    font-size: 2.5rem;
    color: #333;
    margin-bottom: 12px;
  }

  .subtitle {
    font-size: 1.2rem;
    color: #666;
  }
}

.upload-section {
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 24px;
  margin-bottom: 40px;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}

.upload-card {
  background: white;
  border-radius: 16px;
  padding: 40px;
  text-align: center;
  border: 2px dashed #E0E0E0;
  transition: all 0.3s ease;

  &:hover {
    border-color: #3865F2;
  }

  .upload-icon {
    width: 64px;
    height: 64px;
    margin-bottom: 24px;
  }

  h2 {
    font-size: 1.8rem;
    color: #333;
    margin-bottom: 12px;
  }

  p {
    color: #666;
    margin-bottom: 24px;
  }

  @media (max-width: 768px) {
    padding: 24px;
  }
}

.file-input {
  display: none;
}

.upload-btn {
  background: #3865F2;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s ease;

  &:hover {
    background: #2851D8;
    transform: translateY(-2px);
  }

  .icon {
    font-size: 1.2rem;
    font-weight: bold;
  }
}

.info-card {
  background: white;
  border-radius: 16px;
  padding: 32px;
  border: 1px solid #eee;

  h3 {
    font-size: 1.4rem;
    color: #333;
    margin-bottom: 16px;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin-bottom: 24px;

    li {
      color: #666;
      margin-bottom: 12px;
      padding-left: 24px;
      position: relative;

      &::before {
        content: '✓';
        color: #3865F2;
        position: absolute;
        left: 0;
      }
    }
  }

  @media (max-width: 768px) {
    padding: 24px;
  }
}

.supported-formats {
  h4 {
    font-size: 1.1rem;
    color: #333;
    margin-bottom: 12px;
  }
}

.format-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;

  .tag {
    background: #F5F8FF;
    color: #3865F2;
    padding: 4px 12px;
    border-radius: 16px;
    font-size: 0.9rem;
    font-weight: 500;
  }
}

.files-section {
  background: white;
  border-radius: 16px;
  padding: 32px;
  border: 1px solid #eee;
  margin-top: 24px;

  h2 {
    color: #333;
    margin-bottom: 20px;
  }

  @media (max-width: 768px) {
    padding: 24px;
  }
}

.files-list {
  margin-top: 20px;
}

.file-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px;
  border-bottom: 1px solid #eee;

  &:last-child {
    border-bottom: none;
  }
}

.file-info {
  display: flex;
  flex-direction: column;
  gap: 4px;

  .file-name {
    font-weight: 500;
    color: #333;
  }

  .file-size {
    font-size: 0.9rem;
    color: #666;
  }
}

.remove-btn {
  background: transparent;
  color: #DC3545;
  border: 1px solid #DC3545;
  border-radius: 6px;
  padding: 6px 12px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all 0.2s ease;

  &:hover {
    background: #FFF5F5;
  }
}

.actions {
  margin-top: 24px;
  display: flex;
  justify-content: flex-end;
}

.process-btn {
  background: #3865F2;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px 32px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;

  &:hover {
    background: #2851D8;
    transform: translateY(-2px);
  }
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
</style> 