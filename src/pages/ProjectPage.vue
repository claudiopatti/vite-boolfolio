<script>
import axios from 'axios';

export default {
  data() {
    return { 
      defaultUrl: 'http://127.0.0.1:8000/api/projects',
      project: null,
    }
  },
  mounted() {
    this.getProject();
  },
  methods: {
    
    getProject() {
      axios
        .get(this.defaultUrl + '/' + this.$route.params.slug)
        .then((res) => {
            this.project = res.data.project;
            console.log(this.project);
        })
        .catch((err) => {
          console.error(err);

          this.$router.push({ name: 'not-found'});
        });
    },
  },
}
</script>

<template> 
  <div class="container" v-if="project != null">
    <h1>
      {{ project.id }}) {{ project.name }}
    </h1>
    <div class="row">
      <div class=" d-flex justify-content-center">
        <div class="card" style="width: 18rem;">
          <div class="card-body">
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
              <ul>
                <li v-for="technology in project.technologies" :key="technology.id" >{{ technology.name }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use '../assets/scss/partials/variables' as *;


h1 {
  color: $mainColor;
}
</style>

