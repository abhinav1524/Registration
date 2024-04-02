<script lang="ts">
	// import type { addNotification } from 'svelte-notifications';
	// import { toast } from 'svelte-toast';
	import type { Student } from '../Models/Register';
	import { createEventDispatcher, onMount } from 'svelte';
	const dispatch = createEventDispatcher();

	export let studentData: Student;
	export let isEditingValue = false;

	const countries = [
		{ name: 'India', states: ['haryana', 'punjab', 'himachal pradesh'] },
		{ name: 'Japan', states: ['kiyoto', 'osaka', 'hiroshima'] }
	];

	let states: string[] = [];
	let togglecheck = true;
	//validation for form //
	let errorArray = {
		name: '',
		gender: '',
		age: '',
		country: '',
		state: '',
		city: ''
	};

	function handleCountryChange(event: any) {
		const selectedCountryName = event.target.value;
		const foundCountry = countries.filter((country) => country.name === selectedCountryName);
		let selectedCountry = foundCountry || { name: '', states: [] };
		// console.log(selectedCountry);
		states = selectedCountry[0].states;
	}
	function handleFormData() {
		let hasError = false;
		if (studentData.name == '') {
			errorArray.name = 'Please enter the name';
			hasError = true;
		} else {
			errorArray.name = '';
		}

		if (studentData.gender == '') {
			errorArray.gender = 'Please select the gender ';
			hasError = true;
		} else {
			errorArray.gender = '';
		}
		if (studentData.age === 0) {
			errorArray.age = 'Age should be greater than 0';
			hasError = true;
		} else {
			errorArray.age = '';
		}
		if (studentData.country === '') {
			errorArray.country = 'Please choose the country';
			hasError = true;
		} else {
			errorArray.country = '';
		}
		if (studentData.state === '') {
			errorArray.state = 'Please choose the state ';
			hasError = true;
		} else {
			errorArray.state = '';
		}
		if (studentData.city == '') {
			errorArray.city = 'Please enter the city ';
			hasError = true;
		} else {
			errorArray.city = '';
		}
		if (!hasError) {
			dispatch('formData');
		}
	}

	$: {
		console.log(' STUDENT DATA', studentData);
	}
	// flash messages functions //
	// function displayFlashMessage() {
	// 	toast.push('This is a toast message');
	// }
	// console.log(studentData.id)
</script>

<div>
	<form class=" bg-red-50 rounded-md m-5" on:submit={handleFormData}>
		<div class="my-6 mx-20">
			<label for="name" class="text-xl mt-5">Name</label>
			<input
				type="text"
				id="name"
				class="ml-3 p-2 rounded-sm outline-none mt-5"
				class:error={errorArray.name
					? 'focus:invalid:border-red-600 focus:invalid:ring-red-600'
					: ''}
				bind:value={studentData.name}
				on:input={() => (errorArray.name = '')}
			/>
			{#if errorArray.name != ''}
				<p class="text-red-500">{errorArray.name}</p>
			{/if}
		</div>
		<div class="my-2 mx-20">
			<label for="" class="text-xl">Gender</label>
			<input
				type="radio"
				value="male"
				bind:group={studentData.gender}
				class="ml-5 p-2"
				on:input={() => (errorArray.gender = '')}
			/>Male
			<input
				type="radio"
				value="female"
				bind:group={studentData.gender}
				class="ml-5 p-2"
				on:input={() => (errorArray.gender = '')}
			/>Female
			<p class="text-red-500">{errorArray.gender}</p>
		</div>
		<div class="my-4 mx-20">
			<label for="age" class="text-xl">Age</label>
			<input
				type="number"
				id="age"
				class="ml-8 p-2 rounded-sm outline-none"
				class:error={errorArray.age
					? 'focus:invalid:border-red-600 focus:invalid:ring-red-600'
					: ''}
				bind:value={studentData.age}
				on:input={() => (errorArray.age = '')}
			/>
			<p class="text-red-500">{errorArray.age}</p>
		</div>
		<div class="my-4 mx-20">
			<label for="country" class="text-xl">Country</label>
			<select
				bind:value={studentData.country}
				id="country"
				on:change={handleCountryChange}
				class="w-48 p-2"
				class:error={errorArray.country
					? 'focus:invalid:border-red-600 focus:invalid:ring-red-600'
					: ''}
				on:input={() => (errorArray.country = '')}
			>
				{#each countries as option}
					<option value={option.name}>{option.name}</option>
				{/each}
			</select>
			<p class="text-red-500">{errorArray.country}</p>
		</div>
		<div class="my-4 mx-20">
			<label for="states" class="text-xl">State</label>
			<select
				bind:value={studentData.state}
				id="states"
				class="ml-6 w-48 p-2"
				class:error={errorArray.state
					? 'focus:invalid:border-red-600 focus:invalid:ring-red-600'
					: ''}
				on:input={() => (errorArray.state = '')}
			>
				{#each states as state}
					<option value={state}>{state}</option>
				{/each}
			</select>
			<p class="text-red-500">{errorArray.state}</p>
		</div>
		<div class="my-4 mx-20">
			<label for="city" class="text-xl">City</label>
			<input
				type="text"
				id="city"
				class="ml-8 p-2 rounded-sm outline-none"
				class:error={errorArray.city
					? 'focus:invalid:border-red-600 focus:invalid:ring-red-600'
					: ''}
				bind:value={studentData.city}
				on:input={() => (errorArray.city = '')}
			/>
			<p class="text-red-500">{errorArray.city}</p>
		</div>
		<div class="my-4 mx-20">
			<label for="check" class="text-xl">Agree Terms & conditions</label>
			<input type="checkbox" bind:checked={togglecheck} id="check" class="ml-5" />
		</div>
		<div class="my-4 mx-20 flex">
			{#if isEditingValue}
				<button type="submit" class="bg-blue-200 font-bold px-5 py-3 rounded-md mb-10"
					>update</button
				>
			{:else}
				<button class="bg-blue-200 font-bold px-5 py-3 rounded-md mb-10">submit</button>
			{/if}
		</div>
	</form>
</div>

<style>
	.error {
		border: 1px solid red;
		outline: none;
	}
</style>
