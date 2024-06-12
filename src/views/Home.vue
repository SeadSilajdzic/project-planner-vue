<script>
import SingleProject from "@/components/SingleProject.vue";

export default {
    name: 'Home',
    components: {SingleProject},
    data() {
        return {
            projects: [],
            uri: "http://localhost:3000/projects/"
        }
    },
    mounted() {
        fetch(this.uri)
            .then(response => response.json())
            .then(response => this.projects = response)
            .catch(error => console.log(error));
    },
    methods: {
        handleDeleteProject(id) {
            this.projects = this.projects.filter(project => {
                return project.id !== id;
            })
        },

        handleToggleProjectComplete(id) {
            let p = this.projects.find(project => {
                return project.id === id;
            });

            p.complete = !p.complete;
        }
    }
}
</script>

<template>
    <div class="home">
        <h1>Homepage</h1>
        <div v-if="projects.length">
            <div v-for="project in projects" :key="project.id">
                <SingleProject :project="project" @toggleProjectComplete="handleToggleProjectComplete"
                               @deleteProject="handleDeleteProject"/>
            </div>
        </div>
    </div>
</template>