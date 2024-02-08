<template lang="">
    <form @submit.prevent="handleUpdate">
        <label>Title</label>
        <input type="text" v-model="title" required>
        <label>Details</label>
        <textarea v-model="details" required></textarea>
        <button>Update Project</button>
    </form>
</template>
<script>
export default {
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: 'http://localhost:3000/projects/' + this.id
        }
    },
    methods: {
        handleUpdate() {
            const body = {
                title: this.title,
                details: this.details
            }

            fetch(this.uri, {
                method: 'PATCH',
                header: { 'Content-Type': 'application/json' },
                body: JSON.stringify(body)
            })
                .then(() => this.$router.push('/'))
                .catch(err => console.error(err))
        }
    },
    mounted() {
        fetch(this.uri)
            .then(res => res.json())
            .then(data => {
                this.title = data.title
                this.details = data.details
            })
    }
}
</script>
<style lang="">
    
</style>