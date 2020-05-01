<template>
<section>
	<h2>Update User Name</h2>
	<form @submit="update" action="#" method="GET">
	<label for="userId">
	User ID:
	<input type="number" name="id" id="id" v-model="userId">
	</label>

	<label for="name">
	User Name:
	<input type="text" name="name" id="name" v-model="userName">
	</label>

	<input type="submit" value="Update User">
	</form>
	<dl v-if="user">
		<dt>Status</dt>
		<dd>User was successfully updated</dd>
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
	name:'update-user-name',
	data ()
		{
		return {
		userId: '',
		userName: '',
		user: false
		}
	},
	methods: {
	update ( event )
	{ 
		event.preventDefault();
		const userId = parseInt (this.userId );
		const userName = this.userName;

		//Search for the user.
		axios.patch( `/laravel-vue-api/public/api/user/${userId}`, {
		name: userName
		} )
		.then( response => {
			// console.log( response );
			const user = response.data;

			//Store the user in our data
			this.user = user;

			//Clear the name and Id fields
			this.userId = '';
			this.userName = '';

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