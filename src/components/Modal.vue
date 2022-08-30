<template>
		<div class="modal absolute mx-14 mt-56">
			<div class="md:hidden" >
				<img src="../assets/icon-complete.svg" class="block mx-auto mt-40 w-16">
				<span class="mt-10 text-center text-3xl block">THANK YOU!</span>
				<p class="mt-5 block text-center">We've added your card details</p>
				<button class="block mx-auto mt-10 border-2 bg-indigo-900 px-28 py-2 rounded text-white">Continue</button>
			</div>

				<!---screen media---->
		</div>
</template>

<script setup>
 const props = defineProps(['isShowing'])
</script>


<style scoped>
p{
	font-size: 12px;
}
</style>