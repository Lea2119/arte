<template>
	<div>
		<Appbar :isIphone15="isIphone15" />
		<AppbarIOS :isIphone15="isIphone15" />
	</div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue"
import { Device } from "@capacitor/device"
import Appbar from "@/components/Appbars/Appbar.vue"
import AppbarIOS from "@/components/Appbars/AppbarIOS.vue"

const isIphone15 = ref(false)

onMounted(async () => {
	const deviceInfo = await Device.getInfo()
	const iphone15 = deviceInfo.model.toLowerCase().includes("iphone15")
	isIphone15.value = iphone15
})
</script>

<style scoped>
.nav-drawer {
	color: #e4012c;
	font-weight: bold;
}
</style>
