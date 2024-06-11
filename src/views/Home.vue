<template>
    <div class="home">
        <h1>Homepage</h1>
        <div v-if="projects.length">
            <div v-for="project in projects" :key="project.id">
                {{ project.title }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Home',
    components: {},
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
