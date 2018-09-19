<template>
	<div class="box">
		<table border="1">
			<tbody>
				<tr v-for="i in 8">
					<td v-for="j in 8" class="cell" :id="coordinateVal(i,j)"></td>
				</tr>
			</tbody>
		</table>
	</div>
</template>
<script type="text/javascript">
	export default {
		data() {
			return {
				alphabetArr: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h']
			}
		},
		methods: {
			coordinateVal (i, j) {
				let index = j-1;
				let a = this.alphabetArr[index];
				return a + i;
			}
		}
	}
</script>
<style type="text/css">
	.box {padding: 10px; margin-bottom: 1em}
	table {width: 360px; height: 360px; background: green}
</style>