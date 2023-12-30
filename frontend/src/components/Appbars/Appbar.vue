<template>
	<div>
		<v-app-bar v-if="!props.isIphone15" color="#e4012c">
			<template v-slot:prepend>
				<v-app-bar-nav-icon
					variant="text"
					@click.stop="drawer = !drawer"
				></v-app-bar-nav-icon>
			</template>
		</v-app-bar>
		<v-navigation-drawer
			class="nav-drawer d-flex justify-center w-25"
			style="background-color: #e4012c"
			v-model="drawer"
			location="left"
			temporary
		>
			<v-list v-for="(item, index) in filteredItems" :key="index">
				<v-list-item
					style="color: white"
					:prepend-icon="item.icon"
					:title="item.title"
					:value="item.value"
				></v-list-item>
			</v-list>
		</v-navigation-drawer>
	</div>
</template>

<script setup lang="ts">
import { ref, computed, watch, defineProps } from "vue"

const userIsPremium = ref(false)
const userIsAdmin = ref(true)
const group = ref()
const props = defineProps(["isIphone15"])
const drawer = ref(false)

interface Item {
	title: string
	value: string
	icon: string
	account?: string
}

const items = ref<Array<Item>>([
	{
		title: "home",
		value: "home",
		icon: "mdi-home",
	},
	{
		title: "quizzes",
		value: "quizzes",
		icon: "mdi-puzzle",
		account: "premium",
	},
	{
		title: "artists",
		value: "artists",
		icon: "mdi-account",
	},
	{
		title: "artworks",
		value: "artworks",
		icon: "mdi-palette",
	},
	{
		title: "mediums",
		value: "mediums",
		icon: "mdi-brush",
	},
	{
		title: "data facts",
		value: "data facts",
		icon: "mdi-chart-donut",
		account: "premium",
	},
	{
		title: "edit",
		value: "edit",
		icon: "mdi-cog",
		account: "admin",
	},
	{
		title: "account",
		value: "account",
		icon: "mdi-account-circle",
		account: "admin",
	},
])

const filteredItems = computed(() => {
	if (userIsPremium.value) {
		return items.value.filter((item: Item) => item.account !== "admin")
	} else if (userIsAdmin.value) {
		return items.value
	} else {
		return items.value.filter(
			(item: Item) =>
				item.account !== "premium" && item.account !== "admin"
		)
	}
})

watch(group, () => {
	drawer.value = false
})
</script>

<style scoped></style>
