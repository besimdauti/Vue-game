<template>
	<div>
		<form>

			<div class="form-group">
				<label for="exampleFormControlInput1">Player 1 Name</label>
				<input type="email" 
						class="form-control"
						id="exampleFormControlInput1" 
						placeholder="Player 1"
						v-model="playerOne">
			</div>

			<div class="form-group">
				<label for="exampleFormControlInput2">Player 2 Name</label>
				<input type="email" 
						class="form-control" 
						id="exampleFormControlInput2" 
						placeholder="Player 2" 
						v-model="playerTwo">
			</div>

			<div class="form-group">
				<label for="exampleFormControlInput3">Game Length</label>
				<input type="email" 
						class="form-control" 
						id="exampleFormControlInput3" 
						placeholder="e.g. 40" 
						v-model="gameLength">
			</div>

			<div class="form-group">
				<label for="exampleFormControlSelect1">Unlucky Number</label>
				<select class="form-control" 
						id="exampleFormControlSelect1" 
						v-model="unLucky">
					<option>1</option>
					<option>2</option>
					<option>3</option>
					<option>4</option>
					<option>5</option>
					<option>6</option>
				</select>
			</div>

			<button type="submit" class="btn btn-primary" @click.prevent="newGame">Start Game</button>
		</form>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				playerOne: 'Player 1',
				playerTwo: 'Player 2',
				gameLength: 40,
				unLucky: 1
			}
		},
		methods: {
			newGame() {
				this.$emit('startNewGame', this.playerOne, this.playerTwo, this.gameLength, this.unLucky);
			}
		}
	}
</script>

<style scoped>
	form {
		max-width: 600px;
		margin: 0 auto;
	}
</style>