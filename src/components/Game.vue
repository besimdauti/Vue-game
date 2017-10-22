<template>
	<div>
		<div class="container">
			<div class="row">
				<div class="col-sm">
					<div class="alert" role="alert" :class="{ 'alert-success': isActive, 'alert-danger': !isActive }">
						<h3 class="alert-heading">{{ defaultVar[0] }} <span class="right"> {{ playerOneScore }}</span></h3>
						<hr>
						<h5>Here is your curr score: <span class="badge-danger">{{ CurrScoreOne }}</span></h5>
					</div>
				</div>
				<div class="col-sm">
					<div class="alert second-player" role="alert" :class="{ 'alert-success': !isActive, 'alert-danger': isActive }">
						<h3 class="alert-heading">{{ defaultVar[1] }} <span class="left">{{ playerTwoScore }}</span></h3>
						<hr>
						<h5>Here is your curr score: <span class="badge-danger">{{ CurrScoreTwo }}</span></h5>
					</div>
				</div>
			</div>
			<div v-if="!finishState" class="rolling-section alert alert-secondary">
				
                <span alt="Dice" class="dice btn btn-warning">{{ diceValue }}</span>
                <hr>
                <button class="btn-roll btn btn-danger" @click="rollDice"><i class="ion-ios-loop"></i>Roll dice</button>
                <hr>
                <button class="btn-hold btn btn-success" @click="holdPoints"><i class="ion-ios-download-outline"></i>Hold</button>
                
			</div>
			<div v-else class="alert alert-info results-box">
				<h4 class="alert-heading">{{ winner }} won the game!</h4>
				<hr>
				<div class="row">
					<div class="col-sm">
						<ul class="list-group">
							<li 
								class="list-group-item" 
								v-for="(points, index) in playerOneTurns">
									{{ index + 1 }}. {{ defaultVar[0] }} has scored {{ points }}
							</li>
						</ul>
					</div>
					<div class="col-sm">
						<ul class="list-group">
							<li 
								class="list-group-item" 
								v-for="(points, index) in playerTwoTurns">
									{{ index + 1 }}. {{ defaultVar[1] }} has scored {{ points }}
							</li>
						</ul>
					</div>
				</div>
				<hr>
				<button class="btn-roll btn btn-success" @click="resetGame"><i class="ion-ios-loop"></i>New Game</button>
			</div>
		</div>
	</div>
</template>

<script>

    export default {
		props: ['defaultVar'],
		data () {
			return {
				playerOneScore: 0, //Player one score
				playerTwoScore: 0, // Player two score
				CurrScoreOne: 0, //Current score of player one
				CurrScoreTwo: 0, //Current score of player two,
				playerOneTurns: [], // save each turn points in array
				playerTwoTurns: [], // save each turn points in array
				isActive: true, //player active state
				diceValue: 0, //dice value at start
				finish: this.defaultVar[2], // finish points of game
				unLuckyNumber: this.defaultVar[3], //unlucky number
				finishState: false,	// finish state
				winner: this.defaultVar[0]	//win player
			}
		},
		methods: {
			rollDice: function () {

				var randomPoints = Math.max(Math.floor(Math.random() * 6) + 1, 1);

				this.diceValue = randomPoints;

				if (randomPoints != this.unLuckyNumber) {
					this.isActive ? this.CurrScoreOne +=randomPoints : this.CurrScoreTwo +=randomPoints;
				} else {
					this.isActive ? this.playerOneTurns.push(0) : this.playerTwoTurns.push(0);
					this.CurrScoreOne = 0;
					this.CurrScoreTwo = 0;
					this.isActive = !this.isActive;
					this.diceValue = 0;
				}
			},

			holdPoints: function () {
				this.playerOneScore += this.CurrScoreOne;
				this.playerTwoScore += this.CurrScoreTwo;
				this.isActive ? this.playerOneTurns.push(this.CurrScoreOne) : this.playerTwoTurns.push(this.CurrScoreTwo);
				this.CurrScoreOne = 0;
				this.CurrScoreTwo = 0;
				this.diceValue = 0;
				this.checkWinners();
			},

			checkWinners: function() {
				if ( this.playerOneScore >= this.finish || this.playerTwoScore >= this.finish ) {
					this.finishState = true;
					if ( this.playerOneScore >= this.finish ) {
						this.winner = this.defaultVar[0];
					} else {
						this.winner = this.defaultVar[1];
					}
				} else {
					this.isActive = !this.isActive;
				}
			},

			resetGame: function () {
				this.playerOneScore = 0,
				this.playerTwoScore = 0,
				this.CurrScoreOne = 0,
				this.CurrScoreTwo = 0,
				this.playerOneTurns = [],
				this.playerTwoTurns = [],
				this.isActive = true,
				this.diceValue = 0,
				this.finishState = false
			}
		}
    }
</script>

<style scoped>
	span.right {
		float: right;
	}
	span.left {
		float: left;
	}
	h5 {
		margin-top: 60px;
	}
	.second-player .alert-heading {
		text-align: right;
	}
	.rolling-section,
	.results-box {
		max-width: 400px;
		padding: 40px 10px;
		margin: 0 auto;
		text-align: center;
		margin-top: 30px;
	}
	span.dice {
		width: 60px;
		height: 40px;
		display: inline-block;
	}
	button {
		width: 260px;
	}
	h5 span.badge-danger {
		padding: 5px 20px;
	}
	.results-box {
		max-width: 600px;
	}
</style>