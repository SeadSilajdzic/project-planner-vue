<script>
export default {
    name: "AddProject",
    data() {
        return {
            title: '',
            details: '',
            uri: "http://localhost:3000/projects/"
        }
    },

    methods: {
        handleSubmit() {
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            }

            fetch(this.uri, {
                method: "POST",
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(project)
            })
                .then(() => {
                    this.$router.push({name: 'home'})
                })
                .catch(error => console.log(error));
        }
    }
}
</script>

<template>
    <form @submit.prevent="handleSubmit">
        <label>Title</label>
        <input v-model="title" type="text" required>

        <label>Details</label>
        <textarea v-model="details" required></textarea>

        <button>Add project</button>
    </form>
</template>

<style scoped>
form {
    background: white;
    padding: 20px;
    border-radius: 10px;
}

label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}

input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}

textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}

form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
}
</style>