<template>
    <div>
        <div class="loading" v-if="loading">
            <Loading />
        </div>
        <div class="repos">
            <Card v-if="!loading" :href="repo.html_url" :title="repo.name" :body="repo.description" target="_blank" :tags="repo.topics" :forked="repo.fork"
                v-for="repo in repos" :key="repo.id" />
        </div>
    </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';
import Card from './Card.vue';
import Loading from './Loading.vue';

interface Repo {
    id: number;
    name: string;
    html_url: string;
    description?: string;
    topics: string[];
    fork: boolean;
}

export default defineComponent({
    components: {
        Card,
        Loading,
    },

    data() {
        return {
            repos: [] as Repo[],
            loading: true,
        };
    },

    mounted() {
        this.fetchRepos();
    },

    methods: {
        async fetchRepos(): Promise<void> {
            const response = await fetch("https://api.github.com/users/samfelgar/repos?sort=created&direction=desc");
            this.repos = await response.json() as Repo[];
            this.loading = false;
        }
    }
});

</script>

<style>
.loading {
    display: flex;
    min-height: 40rem;
    justify-content: center;
    align-items: center;
}

.repos {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    margin-top: 2rem;
}

@media(max-width: 700px) {
    .repos {
        display: flex;
        flex-direction: column;
        grid-template-columns: unset;
        width: 100%;
    }
}
</style>