/* eslint-disable vue/no-unused-components */
<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @toggleComplete="handleComplete"
        />
      </div>
    </div>
    <div v-else>
      <p>No projects found</p>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  name: "Home",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => response.json())
      .then((data) => (this.projects = data))
      .catch((error) => console.log(error.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      // this.projects = this.projects.map((project) => {
      //   if (project.id === id) {
      //     project.complete = !project.complete;
      //   }
      //   return project;
      // });

      let p = this.projects.find((project) => project.id === id);
      p.complete = !p.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "all") {
        return this.projects;
      }
      return this.projects.filter(
        (project) => project.complete === (this.current === "completed")
      );
    },
  },
};
</script>
