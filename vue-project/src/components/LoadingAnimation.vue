<template>
	<div class="loading-container">
	  <div class="loading-circle"></div>
	</div>
  </template>
  

  <style scoped>
  .loading-container {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: rgb(43, 43, 43);
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 9999; /* Ensure it's above all other content */
  }
  
  .loading-circle {
	background-color: rgb(236, 236, 236);
	border-radius: 50%;
	width: 100px;
	height: 100px;
	/* Initial scale will be 1, but we'll animate this with GSAP */
  }
  </style>
  

  <script>
  import { gsap } from 'gsap';
  
  export default {
	name: 'LoadingAnimation',
	mounted() {
	  // "Breathe" animation
	  gsap.to('.loading-circle', {
		duration: 1.5,
		scale: 1.1, // 10% larger
		repeat: 2, // Repeat this 2 times
		yoyo: true, // Reverts to original size, creating the breathing effect
		onComplete: this.expandCircle // Once breathing is done, expand the circle
	  });
	},
	methods: {
	  expandCircle() {
		// Fully expand the circle to cover the screen
		gsap.to('.loading-circle', {
		  duration: 1,
		  scale: 30, // This value might need to be adjusted depending on the circle's initial size and the screen dimensions
		  onComplete: this.completeLoading
		});
		gsap.to('.loading-container', {
		  duration: 1,
		  backgroundColor: 'white'
		});
	  },
	  completeLoading() {
		// Signal to the parent component that the loading is done.
		// In a real application, you might do something like emit an event or update a Vuex store state.
		this.$emit('loadingComplete');
	  }
	}
  }
  </script>
  


  