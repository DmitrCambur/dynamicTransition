<template>
	<div class="container">
	  <!-- Your title and subtitle here -->
	  <div class="text-content">
		<h1>Title Here</h1>
		<p>Subtitle Here</p>
	  </div>
  
	  <!-- Stippled image on the right -->
	  <stippled-image
		class="stippled"
		:src="imageSrc"
		:width="width"
		:points="n"
		:radius="radius"
		:color="color"
	  ></stippled-image>
	</div>
  </template>
  
  <script type="module">
  // Import the stippled-image custom element
  import 'stippled-image';
  import marcusImage from '@/assets/marcus.png';
  
  export default {
	name: 'VoronoiStippling',
	props: {
	  src: {
		type: String,
		required: true
	  },
	  width: {
		type: Number,
		default: 2000
	  },
	  n: {
		type: Number,
		default: 60000
	  },
	  radius: {
		type: Number,
		default: 0.2
	  },
	  color: {
		type: String,
		default: '#000000'
	  }
	},
	computed: {
	  imageSrc() {
		return this.src === 'marcus.png' ? marcusImage : '';
	  }
	}
  };
  </script>
  
  <style>
  .container {
	display: flex;
	flex-wrap: nowrap;
	align-items: stretch;
	height: 10%; /* Full height of the viewport */
  }
  
  .text-content {
	width: 0%; /* Remaining space for text */
	padding: 10px;
  }
  
  .stippled {
	width: 80%; /* Stippled image takes up 60% width */
	height: 50%; /* Full height of the viewport */
	margin-left: auto; /* Pushes the image to the right */
  }
  </style>
  