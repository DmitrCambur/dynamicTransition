<template>
	<div class="typewriter-container" ref="typewriterContainer">
	  <div class="content">
		<!-- Main Heading -->
		<div class="heading">
		  Marcus Aurelius
		</div>
		<!-- Subtitle -->
		<p class="subtitle">
		  A Stoic Philosopher and Roman Emperor
		</p>
	  </div>
	  <!-- Voronoi Stippling Image Container -->
	  <div class="image-container">
		<!-- Insert VoronoiStippling component here -->
		<VoronoiStippling src="marcus.png" :sampling="1000" :width="1000" :points="50000" :radius="2" :color="'#000'"></VoronoiStippling>
	  </div>
	</div>
	<!-- Placeholder for the next section -->
	<div class="next-section" ref="nextSection" id="next-section">
		<BodyContent />
	</div>
  </template>
  
  <script>
  import { gsap } from "gsap";
  import VoronoiStippling from './VoronoiStippling.vue'; // Adjust the path as necessary
  import BodyContent from './BodyContent.vue'; // Adjust the path as necessary
  
  export default {
	components: {
	  VoronoiStippling,
	  BodyContent
	},
	mounted() {
	  this.animateText();
	  this.setupScrollListener();
	},
	methods: {
	  animateText() {
		const heading = this.$refs.typewriterContainer.querySelector('.heading');
		const subtitle = this.$refs.typewriterContainer.querySelector('.subtitle');
  
		gsap.from(heading, {
		  y: 50,
		  opacity: 1,
		  ease: "easeOut",
		  duration: 2,
		  onComplete: this.emitComplete
		});
  
		gsap.from(subtitle, {
		  y: 50,
		  opacity: 1,
		  ease: "easeOut",
		  duration: 2,
		  delay: 0.5
		});
	  },
	  emitComplete() {
		this.$emit('animationComplete');
	  },
	  setupScrollListener() {
		let scrolled = false;
  
		const scrollHandler = () => {
		  if (!scrolled) {
			const nextSection = this.$refs.nextSection;
  
			if (nextSection) {
			  const offset = nextSection.offsetTop;
			  window.scrollTo({
				top: offset,
				behavior: 'smooth'
			  });
			  scrolled = true;
			}
		  }
  
		  // Remove the event listener after the first scroll
		  window.removeEventListener("scroll", scrollHandler);
		};
  
		// Attach the event listener
		window.addEventListener("scroll", scrollHandler);
	  }
	}
  };
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Lato:wght@100;300;400;700&display=swap');
  
  .typewriter-container {
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: center;
	height: 100vh;
	margin: 0;
	padding: 0;
	max-width: 100vw;
	overflow: hidden;
  }
  
  .content {
	flex: 1;
	padding-left: 5%;
	padding-right: 2.5%;
  }
  
  .heading {
	font-family: 'DM Serif Display', serif;
	font-size: 6rem;
	font-weight: bold;
	line-height: 0.9;
	color: #333;
	margin-bottom: 1rem;
  }
  
  .subtitle {
	font-family: 'Lato', sans-serif;
	font-size: 1.2rem;
	font-weight: 300;
	color: #555;
  }
  
  .image-container {
	flex: 1;
	padding-left: 2.5%;
	display: flex;
	align-items: center;
  }
  
  .scroll-button {
	padding: 10px 20px;
	margin-top: 20px;
	font-size: 1rem;
	cursor: pointer;
	border: 2px solid #333;
	background-color: transparent;
	color: #333;
	transition: all 0.3s ease;
  }
  
  .scroll-button:hover {
	background-color: #333;
	color: #fff;
  }
  
  .next-section {
	background-color: #333;
	color: #fff;
	padding: 100px;
	min-height: 100vh;
  }
  
  .next-section p {
	max-width: 600px;
	margin: 0 auto;
	font-size: 1.5rem;
	line-height: 1.6;
  }
  </style>
  