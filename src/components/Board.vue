<template>
	<div class="box">
		<table border="1">
			<tbody>
				<tr v-for="i in 8">
					<td v-for="j in 8" class="cell" :id="coordinateVal(i,j)">
						<stone v-if="isExist"></stone>
					</td>
				</tr>
			</tbody>
		</table>
	</div>
</template>
<script type="text/javascript">
	import Stone from "./Stone.vue"
	export default {
		data() {
			return {
				alphabetArr: ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'],
				isExist: true
			}
		},
		methods: {
			coordinateVal (i, j) {
				let index = j-1;
				let a = this.alphabetArr[index];
				return a + i;
			}
		},
		components: {
    		Stone
  		}
	}
</script>
<style type="text/css">
	.box {padding: 10px; margin-bottom: 1em}
	.cell {width: 30px; height: 20px; padding: 0;}
	table {width: 360px; height: 360px; background: green; table-layout: fixed;}
</style>