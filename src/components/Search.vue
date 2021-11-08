<template>
	<input type="text" class="form-control rounded" aria-label="Search" aria-describedby="search-addon" v-model="search" placeholder="Search users..." @keyup="getAllPeople" />
	<br />
	<li v-for="person in filterPeopleFeed" :key="person.id"> {{ person.name }} </li>
</template>
<script>
import axios from 'axios';
export default {
	name: 'Search',
	data() {
		return {
			people: [],
			search: ""
		}
	},
	methods: {
		getAllPeople() {
			axios.get('https://jsonplaceholder.typicode.com/users').then(response => {
				this.people = response.data;
			})
		}
	},
	computed: {
		filterPeopleFeed: function() {
			var searchString = this.search;
			var people = this.people;
			// Return nothing when search bar is empty.
			if(!searchString) {
				return ""
			}
			searchString = searchString.trim().toLowerCase();
			people = people.filter(function(item) {
				if(item.name.toLowerCase().indexOf(searchString) !== -1) {
					return item;
				}
			})
			return people;
		}
	}
}
</script>