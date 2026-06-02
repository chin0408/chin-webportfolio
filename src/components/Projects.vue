<script setup>
import ProjectCard from './ProjectCard.vue'
import projects from '../data/projects.json'
</script>

<template>
    <section id="projects" class="projects-dark py-5">
        <div class="container">
            <h2 class="text-center section-title-dark mb-5">My Projects</h2>
            <div class="row g-4">
                <ProjectCard
                    v-for="(project, index) in projects"
                    :key="index"
                    :project="project"
                />
            </div>
        </div>
    </section>
</template>

<script scoped>
</script>



<script scoped>


</script>

