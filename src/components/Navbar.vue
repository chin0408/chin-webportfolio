<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  // Set active on load
  const firstSection = document.querySelector("section")
  if (firstSection) {
    const firstId = firstSection.getAttribute("id")
    document.querySelector(`.nav-link[href="#${firstId}"]`)?.classList.add("active")
  }

  const sections = document.querySelectorAll("section")
  const navLinks = document.querySelectorAll(".nav-link")

  window.addEventListener("scroll", () => {
    let current = ""

    sections.forEach(section => {
      const sectionTop = section.offsetTop - 200   // increase offset threshold
      if (window.scrollY >= sectionTop) {
        current = section.getAttribute("id")
      }
    })

    // Handle bottom of page edge case
    const scrollBottom = window.innerHeight + window.scrollY
    if (scrollBottom >= document.body.offsetHeight - 50) {
      const lastSection = sections[sections.length - 1]
      current = lastSection.getAttribute("id")
    }

    navLinks.forEach(link => {
      link.classList.remove("active")
      if (link.getAttribute("href") === "#" + current) {
        link.classList.add("active")
      }
    })
  })
})
</script>

<template>

	<!-- NAVBAR -->
	<header>
	    <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top custom-navbar">
	      <div class="container">

	        <!-- Logo -->
	        <a class="navbar-brand fw-bold custom-logo" href="#landing">C.M.</a>

	        <!-- Hamburger Button -->
	        <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
	          data-bs-target="#navbarNav" aria-controls="navbarNav"
	          aria-expanded="false" aria-label="Toggle navigation">
	          <span class="navbar-toggler-icon"></span>
	        </button>

	        <!-- Collapsible Menu -->
	        <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
	          <ul class="navbar-nav gap-lg-4">

	            <li class="nav-item">
	              <a class="nav-link" href="#landing">Home</a>
	            </li>

	            <li class="nav-item">
	              <a class="nav-link" href="#projects">My Projects</a>
	            </li>

	            <li class="nav-item">
	              <a class="nav-link" href="#tools">Tools</a>
	            </li>

	            <li class="nav-item">
	              <a class="nav-link" href="#contact">Contact</a>
	            </li>

	          </ul>
	        </div>
	      </div>
	    </nav>
	</header>

</template>


<script scoped>


</script>

