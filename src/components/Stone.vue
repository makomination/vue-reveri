<template>
	<div class="stone"><span v-if="color == 'b'">⚫</span><span v-else="color == 'w'" class="white">⚪</span></div>
</template>
<script type="text/javascript">
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		},
		props: ['color']
	}
</script>
<style type="text/css">
 /*.stone {font-size: 35px; width: 30px; height: 30px; text-align: center;}*/
 .stone {font-size: 30px; text-align: center; margin-left: 5.4px; margin-top: 5.4px; height: 41px; width: 41px;}
 /*.stone .white {background: white;}*/
</style>