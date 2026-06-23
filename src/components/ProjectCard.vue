<script setup>
import { defineProps } from 'vue'

defineProps({
    project: Object
})

function openInLargeWindow(url) {
    const width = 1200
    const height = 800
    const left = (screen.width - width) / 2
    const top = (screen.height - height) / 2
    window.open(url, '_blank', `width=${width},height=${height},left=${left},top=${top},resizable=yes,scrollbars=yes`)
}
</script>

<template>
    <div class="col-lg-4 col-md-6">
        <div class="card project-card-dark h-100 d-flex flex-column">
            <div class="project-image-wrap">
                <img :src="project.image" class="card-img-top" :alt="project.title">
            </div>
            <div class="card-body d-flex flex-column">
                <h5 class="card-title">
                    <span class="project-accent">{{ project.accent }}</span> {{ project.titleRest }}
                </h5>
                <p class="card-text flex-grow-1">{{ project.description }}</p>
                <div class="project-tags">
                    <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                </div>
                <div class="project-actions">
                    <a :href="project.primaryLink" target="_blank" class="project-btn project-btn-primary">
                        {{ project.primaryLabel }}
                    </a>
                    <a :href="project.secondaryLink" @click.prevent="openInLargeWindow(project.secondaryLink)" class="project-btn project-btn-secondary">
                        {{ project.secondaryLabel }}
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
</style>