<template>
	<div>
		<v-bottom-navigation
			mode="shift"
			style="height: 80px"
			grow
			v-if="props.isIphone15"
		>
			<v-btn value="home">
				<v-icon>mdi-home</v-icon>
				<span>home</span>
			</v-btn>
			<v-btn value="recent">
				<v-icon>mdi-magnify</v-icon>
				<span>search</span>
			</v-btn>
			<v-btn value="quizzes">
				<v-icon>mdi-account-circle</v-icon>
				<span>account</span>
			</v-btn>
		</v-bottom-navigation>
	</div>
</template>

<script setup lang="ts">
import { defineProps } from "vue"

const props = defineProps(["isIphone15"])
</script>

<style scoped></style>
