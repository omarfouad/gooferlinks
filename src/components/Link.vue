<template>
  <a class="link-item" @click="onClick(data.title)">
    <div class="link-wrapper">
      <div class="beacon" :id="'beacon_' + data.id" ></div>
      <div class="artwork">
        <img @load="onLoad(data.id)" :id="'image_' + data.id" :src="data.image" alt="">
      </div>
      
      <div class="details">
        <div class="title">{{data.title}}</div>
        <div class="details">{{data.details}}</div>
      </div>
    </div>
  </a>
</template>

<script>
var Notifier = require('../utils/Notifier.js')

export default {
  props: ['data'],
  methods: {
		onClick(e) {
			Notifier("Inner Link (" + e + ")")
			window.location.href = this.data.url
		},

		onLoad(id){
			let image = document.querySelector('#image_' + id)
			let beacon = document.querySelector('#beacon_' + id)

			beacon.style.backgroundColor = this.data.hex
			beacon.style.visibility = "visible"	
		}
	},
}
</script>

<style lang="sass" scoped>


.link-item
	margin-bottom: 20px
	display: block
	cursor: pointer
	

.link-item .link-wrapper:after
	content: ""
	clear: both 
	display: table

.link-item .link-wrapper 
	display: block
	height: 80px
	border-radius: 4px
	padding: 0 10px
	margin-left: 10px
	background-color: #333
	color: white
	position: relative
	transition: all 250ms ease
	&:hover
		background-color: #2f2f2f
		.beacon
			top: 5px
		.artwork
			padding-top: 5px

	& > .beacon
		transition: all 250ms ease
		visibility: hidden
		position: absolute
		border-radius: 4px
		width: 60px
		height: 60px
		top: 10px
		background-color: red
		left: -10px
		animation: beacon 1.8s infinite running
		@media (max-width: 480px)
			left: -20px
		
	& > .artwork
		transition: all 250ms ease
		width: 60px
		height: 60px
		padding: 10px 0
		overflow: hidden
		float: left
		border-radius: 4px
		position: relative
		left: -20px
		@media (max-width: 480px)
			left: -30px
		
		& > img
			width: 100%

	& > .details
		padding: 15px 0px 0px 0px
		float: left
		@media (max-width: 480px)
			position: relative
			left: -15px

		& > .title
			color: #f2f2f2
			word-wrap: break-word
			
		& > .details
			color: #999
			font-size: 14px
			padding: 2px 0

@keyframes beacon
	0%
		opacity: 1
		transform: scale(0)
	50%
		opacity: 0.3
	100%
		transform: scale(1.5)
		opacity: 0
</style>