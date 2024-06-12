<script>
export default {
    name: "SingleProject",
    props: ['project'],
    data() {
        return {
            showDetails: false,
            uri: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods: {
        toggleDetails() {
            this.showDetails = !this.showDetails;
        },

        deleteProject() {
            fetch(this.uri, { method: "DELETE" })
                .then(() => this.$emit('deleteProject', this.project.id))
                .catch(error => console.log(error));
        },

        toggleProjectComplete() {
            fetch((this.uri), {
                method: "PATCH",
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ complete: !this.project.complete })
            })
                .then(() => this.$emit('toggleProjectComplete', this.project.id))
                .catch(error => console.log(error));
        }
    }
}
</script>

<template>
    <div class="project" :class="{ complete: project.complete}">
        <div class="actions">
            <h3 @click="toggleDetails">{{ project.title }}</h3>

            <div class="icons">
                <span class="material-icons">edit</span>
                <span @click="deleteProject" class="material-icons">delete</span>
                <span @click="toggleProjectComplete" class="material-icons" :class="{ tick: project.complete }">done</span>
            </div>
        </div>
        <div v-if="showDetails">
            <p>{{ project.details }}</p>
        </div>
    </div>
</template>

<style scoped>
.project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, .5);
    border-left: 4px solid #e90074;
}

h3 {
    cursor: pointer;
}

.actions {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}

.material-icons:hover {
    color: #777;
}

.project.complete {
    border-left: 4px solid #00ce89;
}

.project.complete .tick {
    color: #00ce89;
}
</style>