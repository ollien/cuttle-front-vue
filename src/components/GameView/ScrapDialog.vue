<template>
	<v-dialog
		v-model="show"
		max-width="750"
		scrollable
	>
		<template
			#activator="{on, attrs}"
		>
			<span
				v-bind="attrs"
				v-on="on"
			>
				<slot name="activator" />
			</span>
		</template>
		<v-card
			id="scrap-dialog"
		>
			<v-card-title class="d-flex justify-space-between">
				<h1>Scrap Pile</h1>
				<v-btn
					icon
					data-cy="close-scrap-dialog-x"
					@click="show=false"
				>
					<v-icon large>
						mdi-close
					</v-icon>
				</v-btn>
			</v-card-title>
			<v-card-text>
				<div class="d-flex flex-wrap justify-center align-center my-8">
					<!-- Empty Placeholder -->
					<template v-if="scrap.length === 0">
						<div class="d-flex flex-column">
							<p>There are no cards in the scrap pile.</p>
							<v-icon x-large>
								mdi-cancel
							</v-icon>
						</div>
					</template>
					<!-- Cards in the scrap -->
					<card
						v-for="(card) in scrap"
						:key="card.id"
						class="mx-1 my-1"
						:suit="card.suit"
						:rank="card.rank"
						:data-scrap-dialog-card="`${card.rank}-${card.suit}`"
					/>
				</div>
			</v-card-text>
			<v-card-actions class="d-flex justify-end my-2">
				<v-btn
					color="primary"
					outlined
					data-cy="close-scrap-dialog-button"
					@click="show=false"
				>
					Close
				</v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>

import Card from '@/components/GameView/Card.vue';

export default {
	name: 'ScrapDialog',
	components: {
		Card,
	},
	props: {
		scrap: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			show: false,
		}
	}
}
</script>

<style lang="scss" scoped></style>
