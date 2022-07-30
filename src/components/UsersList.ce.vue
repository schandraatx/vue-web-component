<template>
	<div>
	<div>
		<input type="text"  @input="this.handleChange" placeholder="Filter by Name"/>
	</div>
	<br/>
	<table class="simple-table">
	<thead>
		<tr>
			<th>Name</th>
			<th>Email</th>
		</tr>
	</thead>
	<tbody>
		<tr v-if="data.length === 0"><td colspan="2"><span class="message"> No results found!</span></td></tr>
		<tr v-else v-for="user in data" v-bind:key="user.id">
			<td>{{user.name}}</td>
			<td>{{user.email}}</td>
		</tr>
	</tbody>
	</table>
	</div>
</template>

<script>
	export default {
		tag: 'users-list',
		name: 'UsersList',
		data() {
			return { 
				originalData: [],
				data: [],
				searchString: ''
			}
		},
		methods: {
			onKeyDown : (event) => {
			if (event.keyCode === 8) {
				this.resetState(event);
			}
			},

			resetState : function (event) {
				this.data = this.originalData.filter(user => user.name.toLowerCase().indexOf(event.target.value.toLowerCase()) !== -1);
				this.searchString = event.target.value;
			},
			handleChange : function(event) {
				this.resetState(event);
			},
			fetchData() {
				fetch('https://jsonplaceholder.typicode.com/users')
				.then(response => {
					if (!response.ok) {
						throw new Error('Network error');
					}
					return response.json();
				})
				.then(data => {
					this.data = data;
					this.originalData = data;
				})
				.catch((error) => {
					console.error('Error:', error);
				});
			}
		},
		created() {
			this.fetchData();
		},
	};
</script>

<style scoped>
	* {
      font-size: 1em;
    }
    .simple-table {
        border: solid 1px #DDEEEE;
        border-collapse: collapse;
        border-spacing: 0;
        font: normal 13px Arial, sans-serif;
    }
    .simple-table thead th {
        background-color: #DDEFEF;
        border: solid 1px #DDEEEE;
        color: #336B6B;
        padding: 10px;
        text-align: left;
        text-shadow: 1px 1px 1px #fff;
    }
    .simple-table tbody td {
        border: solid 1px #DDEEEE;
        color: #333;
        padding: 10px;
        text-shadow: 1px 1px 1px #fff;
    }
	.message {
		font-size: 1.2rem;
		padding:50px;
	}
</style>