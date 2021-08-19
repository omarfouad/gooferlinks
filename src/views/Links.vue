<template>

	<div class="links">
		<links-header v-if="headerReady" :data="headerData"></links-header>

		<div class="link-list">
			<template v-for="link in links">
				<link-item :data="link"></link-item>
			</template>
		</div>

		<div class="copyright">&copy 2021 Goofer - All Rights Reserved.</div>
	</div>
</template>

<script>
var axios = require('axios')

import Link from '../components/Link.vue'
import LinksHeader from '../components/LinksHeader.vue'
import Notifier from '../utils/Notifier.js'

export default {
	created() {
		
		Notifier("Links Page")

		axios.get('/content.json').then((res) => {
			this.headerData = res.data.header_data
			this.links = res.data.links
			this.headerReady = true;
		})
		
	},

	data() {
		return {
			links: [],
			headerData: {},
			headerReady: false
		}
	},

	components: {
		"link-item": Link,
		"links-header": LinksHeader
	}
}
</script>

<style lang="sass">
	.link-list
		padding: 10px 30px
		max-width: 1000px
		margin: 0 auto

	.copyright
		border-top: 1px solid #444
		margin-top: 50px
		text-align: center
		font-size: 12px
		padding-top: 20px
		padding-bottom: 30px
		color: rgba(white, 0.4)

</style>