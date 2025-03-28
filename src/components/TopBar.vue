<script setup>
import Toolbar from 'primevue/toolbar';

defineProps({
	pageState:Object
});

</script>

<template>
	<div class="bar">
		<Toolbar>
			<template #start>
				<img src="/icon.png" width="20" height="20"/>
				<p class="title">GM Screen</p>
			</template>

			<template #center>
				<p class="title">{{ pageState.tabs[pageState.currentPageIndex].name }}</p>
			</template>
		</Toolbar>
	</div>
</template>


<style>

InputText{
	border-width: 1px;
}

.right-box{
	display: flex;
	justify-content: end;
}

.grid{
  display: grid;
  grid-template-columns: auto auto;
  row-gap: 10px;
  column-gap: 10px;
  align-items:right;
}

.bar-button, .dialog-button {
	padding: 0%;
	background-color: transparent;
	border-color: transparent;
}

.dialog-button{
	margin-right: 10px;
}

.bar-button {
	margin-left: 10px;
}

.enabled {
	cursor:pointer;
}

.title{
	font-weight: bold;
	padding-left: 10px;
}


.bar{
	width: 100%;
	margin: auto;
	position:fixed;
	left:0%;
	margin-top: -30px;
	border-width: 0px;
}
</style>