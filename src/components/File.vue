<script setup>
import Card from 'primevue/card';


defineProps({
	icon:String,
	name:String
});

</script>

<template>
	<Card style="width: 120px; overflow: hidden" class="file">
		<template #header>
			<img :src="icon" width="120px" />
		</template>
		<template #title>{{ name }}</template>
	</Card>
</template>


<style>
.file .p-card-body {
	padding-top: 0;
}
</style>