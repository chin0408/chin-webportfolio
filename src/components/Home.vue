<script setup>
	import { onMounted } from 'vue'

	onMounted(() => {
	  const text = "Full Stack Web Developer"
	  let i = 0
	  function typeWriter() {
	    if (i < text.length) {
	      document.getElementById("typing").innerHTML += text.charAt(i)
	      i++
	      setTimeout(typeWriter, 50)
	    }
	  }
	  typeWriter()
	})
</script>

<template>
	<!-- HOME SECTION -->
	<section id="landing" class="home-section">
	    <div class="home-content">
	        <div class="home-text animate-left">
	            <h2>Hi, I am</h2>
	            <h1>Chinee</h1>
	            <h3><span id="typing"></span></h3>
	            <p>
	                I build responsive and scalable web applications using modern 
	                technologies such as HTML, CSS, JavaScript, MongoDB, Express, React, and Node.js.
	            </p>

	            <div class="home-buttons">
	                <a href="#contact" class="btn-primary">Contact Me</a>
	            </div>
	        </div>

	        <div class="home-image animate-right">
	            <div class="image-wrapper">
	                <div class="circle-bg"></div>
	                <img src="/images/Professional_Photo_4_noBG.png" alt="Chinee Profile Photo">
	            </div>
	        </div>
	    </div>
	</section>

</template>

<script scoped>

</script>