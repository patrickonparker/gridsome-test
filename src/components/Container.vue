<template lang="pug">
v-container(
	:data-name="blok.name",
	:class="[full, blok.bottom_margin, blok.shape, blok.class]",
	:style="blok.style",
	v-editable="blok"
)
	component(
		v-for="blok in blok.content",
		:key="blok._uid",
		:blok="blok",
		:is="blok.component"
	)
</template>

<script>
	export default {
		props: ["blok"],
		computed: {
			full() {
				return this.blok.full_width ? "full" : "";
			},
		},
	};
</script>

<style scoped lang="scss">
	.container {
		position: relative;

		@media (min-width: 1024px) {
			padding: 24px;
			max-width: 1440px;
		}

		&.full {
			max-width: none !important;
		}

		&.bottom {
			&-curve {
				-webkit-clip-path: ellipse(100% 60% at 50% 40%);
				clip-path: ellipse(100% 60% at 50% 40%);
			}

			&-arrow {
				-webkit-clip-path: polygon(
					0 0,
					100% 0,
					100% calc(100% - 24px),
					50% 100%,
					0 calc(100% - 24px)
				);
				clip-path: polygon(
					0 0,
					100% 0,
					100% calc(100% - 24px),
					50% 100%,
					0 calc(100% - 24px)
				);
				padding-bottom: 36px;
			}

			&-lean {
				&-left {
					-webkit-clip-path: polygon(0 0, 100% 0, 100% calc(100% - 24px), 0 100%);
					clip-path: polygon(0 0, 100% 0, 100% calc(100% - 24px), 0 100%);
				}

				&-right {
					-webkit-clip-path: polygon(0 0, 100% 0, 100% 100%, 0 calc(100% - 24px));
					clip-path: polygon(0 0, 100% 0, 100% 100%, 0 calc(100% - 24px));
				}
			}
		}

		&.slope {
			&-clockwise {
				-webkit-clip-path: polygon(
					0 0,
					100% 24px,
					100% 100%,
					0 calc(100% - 24px)
				);
				clip-path: polygon(0 0, 100% 24px, 100% 100%, 0 calc(100% - 24px));
			}

			&-counter-clockwise {
				-webkit-clip-path: polygon(
					0 24px,
					100% 0,
					100% calc(100% - 24px),
					0 100%
				);
				clip-path: polygon(0 24px, 100% 0, 100% calc(100% - 24px), 0 100%);
			}
		}
	}
</style>