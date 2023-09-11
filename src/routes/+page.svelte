<script>
	import { createClient } from '@supabase/supabase-js';
	import { onMount } from 'svelte';
	//import Navbar from './navbar.svelte';


	const supabaseUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co';
	const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InNwY2JvY3NpY2JyY3VjdGx3d3FjIiwicm9sZSI6ImFub24iLCJpYXQiOjE2OTMyODQ3NTEsImV4cCI6MjAwODg2MDc1MX0.jK2FAWoHlw6YkDRxuNKWfEeAZYh_OGOjSDkWJqOW2J4';
	const supabase = createClient(supabaseUrl, supabaseKey);


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

	let githubLogoUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co/storage/v1/object/sign/Images/github-mark-white.svg?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cmwiOiJJbWFnZXMvZ2l0aHViLW1hcmstd2hpdGUuc3ZnIiwiaWF0IjoxNjk0NDIzMjAyLCJleHAiOjE3MjU5NTkyMDJ9.m2mQMViFdf7VbYshstMFe3zx0CqRVJQKA8m8HiceT_4&t=2023-09-11T09%3A06%3A42.041Z';

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

//IMAGE ASSETS
	let leftImageUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co/storage/v1/object/sign/Images/PageVector_Left.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cmwiOiJJbWFnZXMvUGFnZVZlY3Rvcl9MZWZ0LnBuZyIsImlhdCI6MTY5NDQzMTE4NiwiZXhwIjoxNzI1OTY3MTg2fQ.Bp7c38YzVGG_xiUPZ_j0Jtg3dCMpDr0NkBQnIxTDQKY&t=2023-09-11T11%3A19%3A45.893Z';
	let rightImageUrl = 'https://spcbocsicbrcuctlwwqc.supabase.co/storage/v1/object/sign/Images/PageVector_Right.png?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1cmwiOiJJbWFnZXMvUGFnZVZlY3Rvcl9SaWdodC5wbmciLCJpYXQiOjE2OTQ0MzEyMDksImV4cCI6MTcyNTk2NzIwOX0.rVE6LispI0yyq-7VgoDQoSSn5DvCR0Rg1ET_cbtFMmA&t=2023-09-11T11%3A20%3A09.073Z';



// Call the handleLogin function when a login action occurs (e.g., button click)
	/* async function handleLoginButtonClick() {
		await handleLogin();
	}*/
	</script> 

<!-- NAVBAR & LOGOS-->

<!--//<Navbar kangLogoUrl={kangLogoUrl} vicLogoUrl={vicLogoUrl} />-->

<div class="navbar">
    <a href="https://www.kangan.edu.au/campus/cremorne/creative-digital-skills-campus">
      <img id="kangLogo" src={kangLogoUrl} alt="Kangan Logo" />
    </a>
    <a href="https://tafe.educationapps.vic.gov.au/s/">
    <img id="vicLogo" src={vicLogoUrl} alt="Tafe Victoria Logo">
    </a>
  </div>

<main>

<!-- HEADER -->
	<h1>Kangan Quiz</h1>
<!-- LOGIN -->

	<div class="form-group">
		<input type="text" placeholder="Username" bind:value="{username}" alt="username" required />
		<input type="password" placeholder="Password" bind:value="{password}" alt="password" />
		<button id="loginButton" on:click="{handleLogin}" alt="login button">Login</button>
		<button id="githubButton" on:click={()=>signInGitHub()} alt="github signin">
		<img src={githubLogoUrl} alt="Github logo" style="height: 1.75em; vertical-align: middle; margin-right: 1em;" />Login with <strong>GitHub</strong></button>
	</div>
</main>

<!-- FOOTER -->
<img class="fixed-left" src={leftImageUrl} alt=""/>
<img class="fixed-right" src={rightImageUrl} alt=""/>

<div class="footer-bar"></div>

<p class="footer-text">&copy; Team Gamma 2023</p>

<style>

@import url('https://fonts.googleapis.com/css2?family=Kanit:wght@800&display=swap');



:global(body) {
	margin: 0;
	font-family: system-ui, sans-serif;
	background-color: #f7f7f7;
}


    .navbar {
      background-color: #f6bc10;
      overflow: hidden;
      position: fixed;
      top: 0;
      width: 100%;
      z-index: 100;
      padding: 0.75em;
      display: flex;
      align-items: center;
      border-bottom: 1.5em solid black;
    }
  
    .navbar img {
      height: auto;
      max-height: 4rem;
      width: auto;
      margin-right: 1rem;
    }


main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}


h1 {
	font-family: 'Kanit', sans-serif;
	color: #b33a0d;
	text-transform: uppercase;
	font-size: 4em;
	font-weight: 800;
}

.form-group {
  margin-bottom: 1rem;
  display: flex; /* Use flexbox */
  flex-direction: column;
  align-items: flex-start;  /* Align items to the start (left) */
  text-align: left; /* Left-align text */
 
}

input {
  flex: 2; /* Take up available space */
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.25rem;
  margin-bottom: 0.5rem;
}

input:focus {
  /*outline: 0;  Disable default focus glow 
  border-color: #f6bc10;*/
  box-shadow: 0 0 0 0.25rem rgba(41, 38, 3, 0.375);
}

button {
  padding: 0.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  width: 100%;
  margin-top: 0.5rem;
  min-height: 10mm;
}

#loginButton {
  background-color: #b33a0d;
  color: #fff;
}

#loginButton:hover {
  background-color: #90300c;
  font-style: italic;
}

#githubButton {
  background-color: #207e0b;
  color: #fff;
}

#githubButton:hover {
  background-color: #134a07;
  font-style: italic;
}

button:hover {
  background-color: #0069d9;
  color: #f6bc10;
}

/*LEFT IMAGE*/
.fixed-left {
    position: fixed;
    left: 0;
    bottom: -3.3em;
    z-index: 1; /* Behind the footer-text */
  }
/*RIGHT IMAGE*/
.fixed-right {
    position: fixed;
    right: 0;
    bottom: -3.3em;
    z-index: 1; /* Behind the footer-text */
  }


  .footer-bar {
    position: fixed; /* sticks it to the bottom */
    bottom: 0; /* places it at the bottom */
    width: 100%;
    height: 5.3em; /* Height of the footer */
    background-color: #000;
    z-index: 0; /* Bottom layer */
}

  .footer-text {
    color: #fff; 
    text-align:right;
    position: fixed;
    right: 1.5em;
    bottom: 1em;
    padding: 1em 0;
    z-index: 3; /* Top layer in front of images*/
}

/* MEDIA QUERIES */

/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {
  h1 {
    font-size: 2em;
  }

  .navbar img {
    max-height: 2rem;
  }

  .footer-text {
    font-size: 0.8em;
  }

  button {
    padding: 0.25rem;
  }

  input {
    padding: 0.25rem;
  }

  .fixed-left, .fixed-right {
    max-width: 50px;
    max-height: 50px;
  }
}

/* Small devices (portrait tablets and large phones, 600px - 900px) */
@media only screen and (min-width: 601px) and (max-width: 900px) {
  h1 {
    font-size: 3em;
  }

  .navbar img {
    max-height: 3rem;
  }

  .footer-text {
    font-size: 1em;
  }

  button {
    padding: 0.5rem;
  }

  input {
    padding: 0.5rem;
  }

  .fixed-left, .fixed-right {
    max-width: 75px;
    max-height: 75px;
  }
}

/* Medium devices (landscape tablets, 901px - 1200px) */
@media only screen and (min-width: 901px) and (max-width: 1200px) {
  /* CSS rules for medium devices */
}

/* Large devices (laptops/desktops, 1201px and up) */
@media only screen and (min-width: 1201px) {
  /* CSS rules for large devices */
  .fixed-left, .fixed-right {
    max-width: 500px;
    max-height: 500px;
  }
  .footer-bar {
	max-height: 3.2rem;
  }
  .footer-text {
	font-size: 1em;
	padding: 0;
  }
}
/* XLarge devices (measurements to come) */
</style>