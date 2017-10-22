<template>
	<div>
		<div class="jumbotron">
			<h1 class="display-3">Roll Game</h1>
			<p class="lead">This game has 2 players.</p>
			<hr class="my-4">
			<p>
				Each Player has his turn. In his turn he rolls a dice as many times as he whishes. Each points get added to his current score.<br>
				During his turn, if the player rolls unlucky number, he lost the turn and all current score. After that, it's the next player's turn.<br>
				Also the player can choose to 'Hold' current score. If the Player does it, current score will be added to his global score points. After that, it's the next player's turn.<br>
				The first player to reach gameLength number on his global score points wins the game.
			</p>
		</div>
	</div>
</template>

<script>
    export default {
    }
</script>