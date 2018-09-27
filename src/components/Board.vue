<template>
	<div class="box">
		<table border="1">
			<tbody>
				<tr v-for="i in 8">
					<td v-for="j in 8" class="cell" :id="coordinateVal(i,j)" @click="putStone(coordinateVal(i,j))">
						<stone v-if="stoneMap[coordinateVal(i,j)] != '-'" :color="stoneMap[coordinateVal(i,j)]"></stone>
					</td>
				</tr>
			</tbody>
		</table>
		<h1 class="result">Black ⚫ : {{ bNum }} - White ⚪ : {{ wNum }}</h1>
	</div>
</template>
<script type="text/javascript">
	import Stone from "./Stone.vue"
	export default {
		data() {
			return {
				alphabetArr: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'],
				stoneMap: {
					a1: '-' ,b1: '-' ,c1: '-' ,d1: '-' ,e1: '-' ,f1: '-' ,g1: '-' ,h1: '-' ,
					a2: '-' ,b2: '-' ,c2: '-' ,d2: '-' ,e2: '-' ,f2: '-' ,g2: '-' ,h2: '-' ,
					a3: '-' ,b3: '-' ,c3: '-' ,d3: '-' ,e3: '-' ,f3: '-' ,g3: '-' ,h3: '-' ,
					a4: '-' ,b4: '-' ,c4: '-' ,d4: 'w' ,e4: 'b' ,f4: '-' ,g4: '-' ,h4: '-' ,
					a5: '-' ,b5: '-' ,c5: '-' ,d5: 'b' ,e5: 'w' ,f5: '-' ,g5: '-' ,h5: '-' ,
					a6: '-' ,b6: '-' ,c6: '-' ,d6: '-' ,e6: '-' ,f6: '-' ,g6: '-' ,h6: '-' ,
					a7: '-' ,b7: '-' ,c7: '-' ,d7: '-' ,e7: '-' ,f7: '-' ,g7: '-' ,h7: '-' ,
					a8: '-' ,b8: '-' ,c8: '-' ,d8: '-' ,e8: '-' ,f8: '-' ,g8: '-' ,h8: '-' ,
				},
				turn: 'b'
			}
		},
		methods: {
			coordinateVal (i, j) {
				let index = j-1;
				let a = this.alphabetArr[index];
				return a + i;
			},
			putStone(coordinateVal) {
				if(this.stoneMap[coordinateVal] !== '-') return;
				if(this.neighborStones(coordinateVal).length == 0) return;
				//this.stoneMap[coordinateVal] = this.turn;
				this.flipStones(coordinateVal);
				//this.changeTurn();
			},
			changeTurn() {
				this.turn == 'b' ? this.turn = 'w' : this.turn = 'b';
			},
			neighborStones(coordinateVal) {
				let a = coordinateVal.split('')[0];
				let ai = this.alphabetArr.indexOf(a);
				let aib = ai - 1;
				let aia = ai + 1;
				let b = parseInt(coordinateVal.split('')[1]);
				let bb = b - 1;
				let ba = b + 1;
				let resultArr = [];
				for(var i = aib ; i <= aia ; i++) {
					for(var j = bb ; j <= ba ; j++) {
						if (i < 0 || j < 1 || i >= 8 || j >8) continue;
						let s = this.alphabetArr[i];
						let c = s + j;
						if (this.stoneMap[c] !== '-') resultArr.push(c);
					}
				}
				return resultArr;
			},
			flipStones(coordinateVal) {
				let neighborStones = this.neighborStones(coordinateVal);
				let that = this;
				//debugger;
				neighborStones.forEach(position => {
					if (that.stoneMap[position] !== that.turn) {
						let alphabetArr = that.alphabetArr;
						let stoneMap = that.stoneMap;
						let turn = that.turn;
						let changeTurn = that.changeTurn;
						let a = coordinateVal.split('')[0];
						let ai = alphabetArr.indexOf(a);
						let b = parseInt(coordinateVal.split('')[1]);
						let positionA = position.split('')[0];
						let positionAi = alphabetArr.indexOf(positionA);
						let positionB = parseInt(position.split('')[1]);
						let flag = false;
						// vertical check
						if (ai == positionAi && b != positionB) {
							if (b - positionB > 0) {
								for (var j = positionB ; j >= 1 ; j--) {
									 var s = alphabetArr[ai];
									 var c = s + j;
									if(stoneMap[c] == turn) {
										for (var k = positionB ; k > j ; k--) {
											 var c2 = s + k;
											stoneMap[c2] = turn;
											flag = true;
										}
									}
								}
							}
							if (b - positionB < 0) {
								for (var j = positionB ; j <= 8 ; j++) {
									 var s = alphabetArr[ai];
									 var c = s + j;
									if(stoneMap[c] == turn) {
										for (var k = positionB ; k < j ; k++) {
											 var c2 = s + k;
											stoneMap[c2] = turn;
											flag = true;
										}
									}
								}
							}
						}
						// horizontal check
						if (ai != positionAi && b == positionB) {
							if (ai - positionAi > 0) {
								for (var i = positionAi ; i >= 0 ; i--) {
									 var sh = alphabetArr[i];
									 var ch = sh + b;
									if(stoneMap[ch] == turn) {
										for (var k = positionAi ; k > i ; k--) {
											 var s2 = alphabetArr[k]
											 var c2 = s2 + b;
											stoneMap[c2] = turn;
											flag = true;
										}
									}
								}
							}
							if (ai - positionAi < 0) {
								for (var i = positionAi ; i <= 7 ; i++) {
									 var sh = alphabetArr[i];
									 var ch = sh + b;
									if(stoneMap[ch] == turn) {
										for (var k = positionAi ; k < i ; k++) {
											 var s2 = alphabetArr[k]
											 var c2 = s2 + b;
											stoneMap[c2] = turn;
											flag = true;
										}
									}
								}
							}
						}
						if (flag) {
							stoneMap[coordinateVal] = turn;
							changeTurn();
						}
						// TODO: diagonally check
					}
				});
			}
		},
		computed: {
			bNum() {
			　return	 Object.values(this.stoneMap).filter(function (element) { return element == 'b'; }).length;
			},
			wNum() {
			　return	 Object.values(this.stoneMap).filter(function (element) { return element == 'w'; }).length;
			}
		},
		components: {
    		Stone
  		},

	}
</script>
<style type="text/css">
	table {background: green; table-layout: fixed;}
	.box {padding: 10px; margin-bottom: 1em}
	.cell {width: 50px; height: 50px; padding: 0;}
	.result {text-align: left;}
</style>