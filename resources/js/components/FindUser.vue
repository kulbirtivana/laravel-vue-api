<template>
<section>
	<h2>Find a User by Id</h2>
	<form @submit="search" action="#" method="GET">
	<label for="userId">
	User ID:
	<input type="number" name="id" id="id" v-model="userId">
	</label>
	<input type="submit" value="Find User">
	</form>
	<dl v-if="user">
	<dt>Name</dt>
	<dd>{{ user.name }}</dd>
	<dt>Email Address</dt>
	<dd>{{ user.email }}</dd>
	</dl>

	<p v-else>
	User not found
	</p>
</section>
</template>

<script>
export default {
	name:'find-user',
	data ()
	{
	return {
	userId: '',
	user: false
	}
	},
	methods: {
	search ( event )
	{ 
		event.preventDefault();
		const userId = parseInt (this.userId );

		//Search for the user.
		axios.get( `/laravel-vue-api/public/api/user/${userId}` )
		.then( response => {
			// console.log( response );
			const user = response.data;

			//Store the user in our data
			this.user = user;
					})

					.catch( error => { 

					this.user = false;

					console.log( error );
					})
	}
	}
}
</script>

<style></style>