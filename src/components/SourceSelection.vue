<template>
	<div class="sourceselection">
		<div class="jumbotron">
			<h2><span class="glyphicon glyphicon-list-alt"></span> New List</h2>
			<h4>Select News Source</h4>
			<select class="form-control" v-on:change="sourceChange1">
				<option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
			</select>
			
			<div v-if="source">
				<h6>{{source.description}}</h6>
				<a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go to {{source.name}} website</a>
			</div>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';
	export default {
		name: 'sourceselection',
		data() {
			return {
				sources: [],
				source: ''
			}
		},
		methods: {
			sourceChange1: function(event) {
				for(var i = 0; i < this.sources.length; i++) {
					if(this.sources[i].id === event.target.value) {
						this.source = this.sources[i];
					}
				}
				this.$emit('sourceChanging', event.target.value);	
			}
		},
		created: function() {
			axios.get(`https://newsapi.org/v1/sources?language=en`)
    			 .then(res => {
    			 	// console.log("response", res);
      				this.sources = res.data.sources
    			 })
		}
	}
</script>