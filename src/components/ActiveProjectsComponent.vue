<template>
  <!-- card  -->
  <div class="card">
    <!-- card header  -->
    <div class="card-header bg-white border-bottom-0 py-4">
      <h4 class="mb-0">Active Projects</h4>
    </div>
    <!-- table  -->
    <div class="table-responsive">
      <table class="table text-nowrap mb-0">
        <thead class="table-light">
          <tr>
            <th>Project name</th>
            <th>Description</th>
            <th>Started Date</th>
            <th>Ended Date</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="project in projects" :key="project.id">
            <td class="align-middle">
              <div class="d-flex align-items-center">
                <!-- <div>
                  <div class="icon-shape icon-md border p-4 rounded-1">
                    <img src="assets/images/brand/dropbox-logo.svg" alt="" />
                  </div>
                </div> -->
                <div class="lh-1">
                  <h5 class="fw-bold mb-1">
                    <a href="#" class="text-inherit">{{
                      project.project_name
                    }}</a>
                  </h5>
                </div>
              </div>
            </td>
            <td class="align-middle">
              <span class="text-muted">{{ project.description }}</span>
            </td>
            <td class="align-middle">
              <span class="badge text-bg-primary">{{
                project.started_at
              }}</span>
            </td>
            <td class="align-middle">
              <span class="badge text-bg-primary">{{ project.ended_at }}</span>
            </td>
            <td class="align-middle">
              <div
                class="d-flex justify-content-center align-items-center gap-1"
              >
                <button
                  class="btn btn-primary"
                  @click="
                    $router.push({
                      name: 'updateProject',
                      params: { projectId: project.id },
                    })
                  "
                >
                  <i class="fa-solid fa-pen-to-square"></i>
                </button>
                <button
                  class="btn btn-danger"
                  @click="deleteProject(project.id)"
                >
                  <i class="fa-solid fa-trash"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  name: "ActiveProjects",
  data() {
    return {
      projects: [],
    };
  },
  computed: {
    ...mapGetters({
      headers: "getHeaders",
    }),
  },
  methods: {
    getAllProjects() {
      this.axios
        .get("/api/projects", {
          headers: this.headers,
        })
        .then((response) => {
          this.truncateDescription(response.data.projects);
          this.projects = response.data.projects;
        })
        .catch((e) => console.log(e));
    },
    truncateDescription(projects) {
      projects.forEach((element) => {
        if (element.description.length > 15) {
          element.description = element.description.slice(0, 15) + "...";
        }
      });
    },
    deleteProject(projectId) {
      this.axios
        .delete(`/api/projects/${projectId}`, {
          headers: this.headers,
        })
        .then((response) => {
          if (response.data.isDeleted) {
            location.reload();
          }
        })
        .catch((e) => console.log(e));
    },
  },
  mounted() {
    this.getAllProjects();
  },
};
</script>
