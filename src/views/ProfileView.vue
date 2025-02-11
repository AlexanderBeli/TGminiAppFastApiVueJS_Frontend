<template>
    <div class="profile-container">
        <h2>Профиль</h2>
        <div class="profile-info">
            <p><strong>ID:</strong> {{ user.id }}</p>
            <p><strong>Имя:</strong> {{ user.name }}</p>
            <p><strong>Выполнено задач:</strong> {{ user.completedTasks }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ProfileView',
    data() {
        return {
            user: {
                id: '',
                name: '',
                completedTasks: 0
            }
        }
    },
    async mounted() {
        await this.fetchProfile()
    },
    methods: {
        async fetchProfile() {
            try {
                const tg_user = window.Telegram.WebApp.initDataUnsafe?.user
                const response = await fetch(`https://orange-sniffle-4xr5qq5g69wfq4wq-8000.app.github.dev/api/main/${tg_user.id}`)
                const data = await response.json()
                this.user.id = tg_user.id
                this.user.name = tg_user.name
                this.user.completedTasks = data.completedTasks
            } catch (error) {
                console.log('error', error)
            }
        }
    }
}
</script>