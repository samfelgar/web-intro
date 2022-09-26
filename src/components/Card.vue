<template>
	<div class="link-card">
		<a :href="href" :target="target ?? '_self'">
			<h3>
				{{title}}
				<span class="fork-info" v-if="forked">(forked)</span>
				<span class="arrow">&raquo;</span>
			</h3>
			<p>
				{{body}}
			</p>
			<div class="tags">
				<span class="tag" v-for="tag in tags" :key="tag">{{ tag }}</span>
			</div>
		</a>
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue"


export default defineComponent({
	props: {
		href: String,
		target: { type: String, required: false },
		title: String,
		body: String,
		tags: { type: Array, required: false },
		forked: Boolean,
	}
});

</script>

<style scoped>
.link-card {
	display: flex;
	padding: 0.15rem;
	border-radius: 0.5rem;
	background-position: 100%;
}

.link-card>a {
	width: 100%;
	text-decoration: none;
	line-height: 1.4;
	padding: 1em 1.3em;
	border-radius: 0.35rem;
	color: var(--primary);
	background-color: white;
	opacity: 0.9;
}

h3 {
	margin: 0;
	transition: color 0.6s cubic-bezier(0.22, 1, 0.36, 1);
}

p {
	margin-top: 0.75rem;
	margin-bottom: 0;
}

h3 .arrow {
	display: inline-block;
	transition: transform 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}

.link-card:is(:hover, :focus-within) {
	background-position: 0;
	box-shadow: 0.3rem 0.3rem 2rem .2rem rgba(0, 0, 0, 0.2);
}

.link-card:is(:hover, :focus-within) h3 {
	color: var(--info);
}

.link-card:is(:hover, :focus-within) h3 .arrow {
	will-change: transform;
	transform: translateX(1rem);
}

.tags {
	display: flex;
	gap: .2rem;
	flex-wrap: wrap;
	margin-top: .5rem;
}

.tag {
	background-color: var(--info);
	padding: .15rem .5rem;
	color: #fff;
	border-radius: .3rem;
	font-size: .9rem;
}

.fork-info {
	color: var(--info);
	margin-right: .5rem;
	font-size: .8rem;
}
</style>
