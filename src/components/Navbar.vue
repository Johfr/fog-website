<script setup>
import FogImg from '../components/FogImg.vue'
</script>

<template>
	<nav>
		<p class="logo">Glaciaria</p>

		<ul class="list">
			<li>About</li>
			<li>Blog</li>
			<li>
				<button>
					Sign up
				</button>
			</li>
		</ul>
	</nav>
</template>

<style lang="scss" scoped>
nav {
	min-width: 80%;
	max-width: 80%;
	margin-left: auto;
	margin-right: auto;
    display: flex;
    justify-content: space-between;
	color: #000;
	position: relative;
	z-index: 3;
	font-family: 'Philosopher', sans-serif;
	text-transform: uppercase;
	animation: slideDown 3s 1s forwards;
	opacity: 0;

	.logo {
		letter-spacing: 5px;
	}

	.list {
		display: flex;
		align-items: center;

		li {
			&:not(:last-child) {
				margin-right: 30px;
			}
		}
	}
}

.fog {
    width: 100%;
    height: 60vh;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1;

}

@keyframes slideDown {
	from {
		transform: translateY(-100px);
		opacity: 0;
	}
	to {
		transform: translateY(0);
		opacity: 1;
	}
}
</style>
