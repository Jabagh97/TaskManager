<template>
  <div class="project">
    <v-card>
      <v-card-title>Projeler</v-card-title>

      <div v-for="project in projects" :key="project.id">
        <v-row class="ma-0 pb-5 px-2">
          <v-col>
            <h1>
              <router-link :to="{ path: '/PeriodTasks', query: { projectKey: project.key, siteId,siteUrl } }">
                <v-btn color="primary" x-large>
                  {{ project.name }}
                </v-btn>
              </router-link>
            </h1>
          </v-col>
          <v-col>
            <h3>Proje Anahtarı :{{ project.key }}</h3>
          </v-col>
        </v-row>
      </div>
    </v-card>
  </div>
</template>
<script>
import Project from '@/clients/Project'

export default {
  name: 'ProjectView',
  data() {
    return { projects: [], message: '', siteId: null, siteUrl: "" }
  },
  async mounted() {
    this.siteId = this.$route.query.siteId
    this.siteUrl = this.$route.query.siteUrl
    this.loadProjects(this.siteId)
  },
  methods: {
    async loadProjects(siteId) {
      const { data } = await Project.get(siteId)
      this.projects = data
    },
  },
}
</script>

