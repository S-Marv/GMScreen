<script setup>
defineProps({
	height:NaN,
	src: String,
	rotation:NaN
})

</script>

<template>
	<button class="image-button"><img :src="src" :height="height" :style="rotation? 'rotate:'+rotation : ''"></img></button>
</template>


<style>
.image-button {
	padding: 0%;
	background-color: transparent;
	border-color: transparent;
}

.enabled {
	cursor:pointer;
}
</style>