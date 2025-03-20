<template>
  <BaseLayout>
    <div class="projects">
      <div class="header">
          <h1>{{ $t('projects') }}</h1>
          <button class="new-project-btn" @click="showCreateModal = true">
          <span class="icon">+</span>
          New Project
        </button>
      </div>

      <div class="projects-grid" v-if="projects.length">
        <div v-for="project in projects" :key="project.id" class="project-card">
          <div class="project-header">
            <h3>{{ project.name }}</h3>
            <span class="status" :class="project.status">{{ project.status }}</span>
          </div>
          <p class="description">{{ project.description }}</p>
          <div class="meta">
            <span class="date">Created: {{ formatDate(project.createdAt) }}</span>
            <span class="files">Files: {{ project.filesCount }}</span>
          </div>
          <div class="actions">
            <button class="action-btn view" @click="viewProject(project.id)">
              View Details
            </button>
            <button class="action-btn edit" @click="editProject(project.id)">
              Edit
            </button>
          </div>
        </div>
      </div>

      <div v-else class="empty-state">
        <img src="../assets/empty-projects.svg" alt="No projects" class="empty-icon" />
        <h2>No Projects Yet</h2>
        <p>Create your first project to start managing your data processing tasks</p>
        <button class="new-project-btn" @click="showCreateModal = true">
          <span class="icon">+</span>
          Create Project
        </button>
      </div>
    </div>
  </BaseLayout>
</template>

<script>
import BaseLayout from '../layouts/BaseLayout.vue';

export default {
  name: 'Projects',
  components: {
    BaseLayout
  },
  data() {
    return {
      projects: [
        {
          id: 1,
          name: 'Customer Data Anonymization',
          description: 'Anonymizing customer database for analytics',
          status: 'active',
          createdAt: '2024-03-20',
          filesCount: 3
        },
        {
          id: 2,
          name: 'Employee Records',
          description: 'Processing HR data for compliance',
          status: 'completed',
          createdAt: '2024-03-15',
          filesCount: 5
        }
      ]
    }
  },
  methods: {
    formatDate(date) {
      return new Date(date).toLocaleDateString()
    },
    viewProject(id) {
      console.log('Viewing project:', id)
    },
    editProject(id) {
      console.log('Editing project:', id)
    }
  }
}
</script>

<style lang="scss" scoped>
.projects {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
}

h1 {
  font-size: 2.5rem;
  color: #333;
  margin: 0;
}

.new-project-btn {
  background: #3865F2;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  display: flex;
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

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 24px;
}

.project-card {
  background: white;
  border-radius: 16px;
  padding: 24px;
  border: 1px solid #eee;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  }
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;

  h3 {
    font-size: 1.2rem;
    color: #333;
    margin: 0;
  }
}

.status {
  font-size: 0.875rem;
  padding: 4px 12px;
  border-radius: 12px;
  font-weight: 500;

  &.active {
    background: #E3F2FD;
    color: #1976D2;
  }

  &.completed {
    background: #E8F5E9;
    color: #2E7D32;
  }
}

.description {
  color: #666;
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 16px;
}

.meta {
  display: flex;
  gap: 16px;
  font-size: 0.875rem;
  color: #666;
  margin-bottom: 16px;
}

.actions {
  display: flex;
  gap: 12px;
}

.action-btn {
  flex: 1;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;

  &.view {
    background: #F5F5F5;
    color: #333;
    border: 1px solid #E0E0E0;

    &:hover {
      background: #EEEEEE;
    }
  }

  &.edit {
    background: transparent;
    color: #3865F2;
    border: 1px solid #3865F2;

    &:hover {
      background: #F5F8FF;
    }
  }
}

.empty-state {
  text-align: center;
  padding: 60px 20px;

  .empty-icon {
    width: 120px;
    height: 120px;
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
}

@media (max-width: 768px) {
  .projects {
    padding: 20px;
  }

  .header {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }

  h1 {
    font-size: 2rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>