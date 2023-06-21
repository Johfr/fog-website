<script setup>
import Navbar from '../components/Navbar.vue'
import YoutubeIcon from '../components/YoutubeIcon.vue'
import TwitterIcon from '../components/TwitterIcon.vue'
import InstaIcon from '../components/InstaIcon.vue'
import { ref, onMounted, onUnmounted } from 'vue'

const targetSection = ref(null)
let entryObserver
let exitObserver
let animateSection = ref(false)

onMounted(() => {
  const options = {
    threshold: [0.35]
  }

  entryObserver = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        handleTargetSectionVisible()
      }
    })
  }, options)

  entryObserver.observe(targetSection.value)

  const exitOptions = {
    threshold: [0.34]
  }

  exitObserver = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (!entry.isIntersecting) {
        handleTargetSectionExit()
      }
    })
  }, exitOptions)

  exitObserver.observe(targetSection.value)
})

onUnmounted(() => {
  if (entryObserver) {
    entryObserver.disconnect()
  }
  
  if (exitObserver) {
    exitObserver.disconnect()
  }
})

function handleTargetSectionVisible() {
  console.log('La section cible est visible à 35%')
  animateSection.value = true
}

function handleTargetSectionExit() {
  console.log('La section cible est sortie des 35%')
  animateSection.value = false
}

const scrollToSection2 = () => {
  if (targetSection.value) {
    targetSection.value.scrollIntoView({ behavior: 'smooth'})
  }
}

</script>

<template>
	<div class="home">
		<Navbar />
		<div class="home-container">
			<img class="fog" src="../assets/img/fog.png" />
			<section class="home-content">
				<div class="title-container">
					<p class="entete">Discover</p>
					<h1 class="title-h1">Himalaya</h1>
				</div>
				<div class="cta-container">
					<div class="rs-container">
						<YoutubeIcon title="Youtube" />
						<TwitterIcon title="Twitter" />
						<InstaIcon title="Insta" />
					</div>
					<p class="cta" @click="scrollToSection2">~Scroll</p>

					<div class="slide-number-container">
						<p>01</p>
						<p>05</p>
					</div>
				</div>

			</section>
		</div>

		<section class="content-section" ref="targetSection">
			<h2 :class="{fade: animateSection}">
				<span>Top</span>
				<span>Destination</span>
			</h2>

			<div class="img-container">
				<img src="../assets/img/air-balloon.jpg" alt="air-balloon" :class="{translate: animateSection}">
				<img src="../assets/img/monument.jpg" alt="monument">
				<img src="../assets/img/lighthouse.jpg" alt="lighthouse" :class="{translate: animateSection}">
			</div>

			<p class="text-content">
				L'Himalaya, cette imposante chaîne de montagnes située en Asie, est un véritable joyau de la nature. S'étendant sur une distance impressionnante de plus de 2 400 kilomètres, elle traverse plusieurs pays, dont le Népal, l'Inde, le Bhoutan et le Tibet. Avec ses sommets majestueux et ses paysages à couper le souffle, l'Himalaya est depuis longtemps une source d'inspiration pour les aventuriers, les alpinistes et les amateurs de nature.

				Les sommets les plus emblématiques de l'Himalaya incluent l'Everest, le Kanchenjunga, le Makalu et l'Annapurna. Ces géants de roche et de glace défient les limites de l'altitude, attirant les alpinistes du monde entier qui rêvent de conquérir ces sommets mythiques.
			</p>
		</section>
	</div>
</template>

<style lang="scss" scoped>

.content-section {
	min-height: 100vh;
	padding-top: 50px;
	padding-bottom: 50px;
	transition: .4s ease;
	background-color: #000;
	color: #fff;

	h2 {
		margin-top: 0;
		font-size: 4rem;
		text-align: center;
		text-transform: uppercase;
  		font-family: 'Merriweather', serif;
		opacity: 0;

		&.fade {
			animation: fade 2s forwards;
		}
		span {
			&:first-child {
				font-weight: 700;
				font-style: italic;
			}
			&:last-child {
				margin-left: 15px;
			}
		}
	}

	.img-container {
		display: flex;
		justify-content: space-between;
		align-items: center;
		max-width: 1080px;
		margin: 75px auto;
		gap: 30px;
		img {
			max-width: 33%;
			transition: 2s ease;

			&:first-child {
				transform: translateX(-300px);
				&.translate {
					transform: translateX(0);
				}
			}
			&:last-child {
				transform: translateX(300px);
				&.translate {
					transform: translateX(0);
				}
			}
		}
	}

	.text-content {
		max-width: 50%;
		margin-left: auto;
		margin-right: auto;
		font-size: 0.8rem;
		text-align: center;
	}
}
.home {
	min-height: 100vh;
	max-height: 100vh;
	overflow-x: hidden;
	position: relative;
}
.home-container {
	background-image: url('../assets/img/himalayas-4k_black-and-white.jpg');
    background-position: 20% 44%;
	background-attachment: fixed;
}

.home-content {
	width: 100%;
	min-height: calc(100vh - 72px);
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	position: relative;
	z-index: 2;
	text-align: center;

	.entete {
		margin-bottom: 75px;
		font-size: 1.5rem;
		font-family: 'Merriweather', sans-serif;
		text-transform: uppercase;
		letter-spacing: 5px;
		animation: slideUp 3s forwards;
	}
	h1 {
		font-size: 4rem;
		font-family: 'Philosopher', sans-serif;
		text-transform: uppercase;
		letter-spacing: 45px;
	}

	.cta-container {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		min-width: 80%;
		max-width: 80%;
		margin-left: auto;
		margin-right: auto;
		color: #fff;
		animation: slideUp 3s 1s forwards;
		opacity: 0;

		.rs-container {
			display: flex;
			justify-content: center;
			align-items: flex-end;
			min-width: 33%;
			margin-top: 130px;

			svg {
				height: 20px;
				width: auto;
				margin-right: 20px;
				fill: #fff;
				cursor: pointer;
				transition: .4s ease;
				opacity: .7;

				&:hover {
					filter: drop-shadow( 0 0 3px #0091b2);
					opacity: 1;
				}
			}
		}
		.cta {
			min-width: 33%;
			margin-top: 0;
			margin-bottom: 75px;
			font-size: 2.1rem;
			font-family: 'Philosopher', sans-serif;
			text-transform: uppercase;
			letter-spacing: 15px;
			position: relative;
			color: #fff;
			cursor: pointer;

			&::after {
				content: "";
				width: 1px;
				height: 100px;
				background-color: #fff;
				position: absolute;
				bottom: -110px;
				left: 50%;
				opacity: .5;
			}

			&:hover {
				&::after {
					opacity: 1;
				}
			}
		}
		.slide-number-container {
			display: flex;
			justify-content: center;
    		align-items: flex-end;
			min-width: 33%;
			margin-top: 110px;
			font-family: 'Philosopher', sans-serif;

			p {
				margin-top: 0;
				margin-bottom: 0;
				font-size: 6rem;
    			line-height: 0.7;

				&:last-child {
					margin-left: 120px;
					font-size: 1.5rem;
					position: relative;

					&::before {
						content: "";
						width: 100px;
						height: 1px;
						background-color: #fff;
						position: absolute;
						bottom: 0;
						left: -110px;
					}
				}
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
	animation: reduce 3s forwards;
}

@keyframes fade {
	from {
		transform: translateY(100px);
		opacity: 0;
	}
	to {
		transform: translateY(0);
		opacity: 1;
	}
}
@keyframes reduce {
	from {
		transform: scale(7.5);
	}
	to {
		transform: scale(1.3);
	}
}
@keyframes slideUp {
	0% {
		transform: translateY(200px);
		opacity: 0;
	}
	70% {
		opacity: 0.3;
	}
	100% {
		transform: translateY(0);
		opacity: 1;
	}
}
</style>
