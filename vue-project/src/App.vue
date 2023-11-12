<template>
	<div>
	  <LoadingAnimation v-if="isLoading" @loadingComplete="onLoadingComplete" />
	  <TypewriterHeading v-if="!isLoading" />

	  <!-- other components or content if any -->
	</div>
  </template>
  
  <script>
  import LoadingAnimation from '@/components/LoadingAnimation.vue';
  import TypewriterHeading from '@/components/TypewriterHeading.vue';
  
  export default {
	data() {
	  return {
		isLoading: true
	  };
	},
	components: {
	  LoadingAnimation,
	  TypewriterHeading
	},
	methods: {
	  onLoadingComplete() {
		this.isLoading = false;
	  }
	}
  }
  </script>
  