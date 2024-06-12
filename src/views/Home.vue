<script>
import SingleProject from "@/components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
    name: 'Home',
    components: {FilterNav, SingleProject},
    data() {
        return {
            projects: [],
            uri: "http://localhost:3000/projects/",
            currentFilter: 'all'
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
    },
    computed: {
        filteredProjects() {
            if(this.currentFilter === 'completed') {
                return this.projects.filter(project => project.complete)
            }

            if(this.currentFilter === 'uncompleted') {
                return this.projects.filter(project => !project.complete)
            }

            return this.projects;
        }
    }
}
</script>

<template>
    <div class="home">
        <FilterNav @filterChange="currentFilter = $event" :current="currentFilter"/>
        <div v-if="projects.length">
            <div v-for="project in filteredProjects" :key="project.id">
                <SingleProject :project="project" @toggleProjectComplete="handleToggleProjectComplete"
                               @deleteProject="handleDeleteProject"/>
            </div>
        </div>
    </div>
</template>