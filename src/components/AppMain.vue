<script>
import axios from 'axios';

export default {
  data() {
    return { 
      projects: [],
      prevPage: null,
      nextPage: null,
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects() {
      axios
        .get('http://127.0.0.1:8000/api/projects')
        .then((res) => {
          this.projects = res.data.projects.data;
          console.log(this.projects);

          this.prevPage = res.data.projects.prev_page_url;
          console.Iog(this.prevPage) ;
          this.nextPage = res.data.projects.next_page_url;
          console.Iog(this.nextPage) ;
        });
    },
    getPrevPage() {
      axios
        .get(this.prevPage)
        .then((res) => {
          this.projects = res.data.projects.data;
          console.log(this.projects);

          this.prevPage = res.data.projects.prev_page_url;
          console.Iog(this.prevPage) ;
          this.nextPage = res.data.projects.next_page_url;
          console.Iog(this.nextPage) ;
        });
    },
    getNextPage() {
      axios
        .get(this.nextPage)
        .then((res) => {
          this.projects = res.data.projects.data;
          console.log(this.projects);

          this.prevPage = res.data.projects.prev_page_url;
          console.Iog(this.prevPage) ;
          this.nextPage = res.data.projects.next_page_url;
          console.Iog(this.nextPage) ;
        });
    },
  }
}
</script>

<template>
  <main>
    <div class="container">
      <div class="row">
        <div v-for="project in projects" :key="project.id" class="col-12 col-sm-12 col-md-6 col-lg-4 g-3">
          <div class="card" style="width: 18rem;">
            <div class="card-body">
              <h5 class="card-title">{{ project.name }}</h5>
              <h6 v-if="project.type != null" class="card-subtitle mb-2 text-body-secondary">
                {{ project.type.name }}
              </h6>
              <h6 v-else class="card-subtitle mb-2 text-body-secondary">
                Non ha un tipo
              </h6>
              <p class="card-text">{{ project.description }}</p>
              <!-- <p v-for="technology in project.technologies" :key="technology.id" class="card-text">{{ technology.name }}</p> -->
              <div>
                <h5>
                  Tecnologie:
                </h5>
              </div>
              <ul >
                <li v-for="technology in project.technologies" :key="technology.id" >{{ technology.name }}</li>
              </ul>
            </div>
          </div>
        </div>
        <div class="btn-group mt-4" role="group" aria-label="Basic example">
          <button @click="getPrevPage()" type="button" class="btn btn-primary mx-4">&lt; Pagina Precedente</button>
          <button @click="getNextPage()" type="button" class="btn btn-primary mx-4">Pagina Successiva &gt;</button>
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
@use '../assets/scss/partials/variables' as *;

main {
  background-color: $mainBgColor;
  text-align: center;
  padding: 20px 0;
}

</style>
