<script>
	import { createClient } from '@supabase/supabase-js'
	import { onMount } from 'svelte';
	import Navbar from './navbar.svelte';


	const supabaseUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co'
	const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InNwY2JvY3NpY2JyY3VjdGx3d3FjIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTMyODQ3NTEsImV4cCI6MjAwODg2MDc1MX0.jK2FAWoHlw6YkDRxuNKWfEeAZYh_OGOjSDkWJqOW2J4'
	const supabase = createClient(supabaseUrl, supabaseKey)


//NAVBAR IMAGES
	let kangLogoUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co/storage/v1/object/sign/Images/Kangan_logo.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cmwiOiJJbWFnZXMvS2FuZ2FuX2xvZ28ucG5nIiwiaWF0IjoxNjk0NDAyMDg3LCJleHAiOjE3MjU5MzgwODd9.aJVXb8Fd6I1fAXIqUnsJedfiz7L1P34iFSE8Z9wXYIE&t=2023-09-11T03%3A14%3A47.742Z';

	let vicLogoUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co/storage/v1/object/sign/Images/tafe_vic.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cmwiOiJJbWFnZXMvdGFmZV92aWMucG5nIiwiaWF0IjoxNjk0MzE0NTkwLCJleHAiOjE3MjU4NTA1OTB9.ECX_cDtQ7R9WbICaD0UDTWzjwDxgpcuatQitjqeYRr4&t=2023-09-10T02%3A56%3A30.325Z';

//LOGIN INPUTS

	let username = '';
	let password = '';

//ON MOUNT SYNC
	onMount(async () => {
    user = await supabase.auth.getUser();
    console.log("onMount -> user:", user);

    if (user) {
        console.log("onMount -> user:", user);
    } else {
        user = null;
    }
});

//USER SIGN IN FUNCTION
	async function handleLogin() {
		const userType = 'Admin'; // Replace with your logic to determine the user type

		if (userType === 'Admin') {
		await handleAdminLogin();
		} 
		else if (userType === 'User') {
		await handleUserLogin();
		} 
		else {
		console.error('Invalid user type.');
		}
	}

// GITHUB SIGN IN FUNCTION
	async function signInGitHub() {
    console.log("signInGitHub");
    const { data, error } = await supabase.auth.signInWithOAuth({
        provider: 'github',
    });
    if(data) {
        console.log("data:", data);
        user = await supabase.auth.getUser();
        console.log("user:", user);
    }
    if(error) {
        console.log("error:", error);
    }
}
async function signout() {
    const { error } = await supabase.auth.signOut();
    if(error) {
        console.log("error:", error);
    }
    user = null;
}


// Call the handleLogin function when a login action occurs (e.g., button click)
	/* async function handleLoginButtonClick() {
		await handleLogin();
	}*/
	</script> 

<!-- NAVBAR & LOGOS-->

<Navbar kangLogoUrl={kangLogoUrl} vicLogoUrl={vicLogoUrl} />


<main>

<!-- HEADER -->
	<h1>Kangan Quiz</h1>
<!-- LOGIN -->

	<div>
	<!-- Other content -->
		<input type="text" placeholder="Username" bind:value="{username}" />
		<input type="password" placeholder="Password" bind:value="{password}" />
		<button on:click="{handleLogin}">Login</button>
		<button on:click={()=>signInGitHub()}>GitHub SignIn</button>
	</div>
</main>

<style>

@import url('https://fonts.googleapis.com/css2?family=Kanit:wght@800&display=swap');



:global(body) {
	margin: 0;
	font-family: system-ui, sans-serif;
	background-color: #f7f7f7;
}

main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

/*main {
	text-align: center;
	padding: 1em;
	max-width: 240px;
	margin: 0 auto;
}*/

h1 {
	font-family: 'Kanit', sans-serif;
	color: #e64610;
	text-transform: uppercase;
	font-size: 4em;
	font-weight: 800;
}

@media (min-width: 640px) {
	main {
	max-width: none;
	}
}

</style>