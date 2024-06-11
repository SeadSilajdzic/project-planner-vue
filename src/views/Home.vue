<template>
    <div class="home">
        <h1>Homepage</h1>
        <div v-if="projects.length">
            <div v-for="project in projects" :key="project.id">
                <SingleProject :project="project"/>
            </div>
        </div>
    </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";

export default {
    name: 'Home',
    components: {SingleProject},
    data() {
        return {
            projects: []
        }
    },
    mounted() {
        fetch("http://localhost:3000/projects")
            .then(response => response.json())
            .then(response => this.projects = response)
            .catch(error => console.log(error));
    }
}
</script>
