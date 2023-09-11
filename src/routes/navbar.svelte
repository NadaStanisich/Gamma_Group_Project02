<script>
    export let kangLogoUrl;
    export let vicLogoUrl;
</script>
  
<style>
    .navbar {
      background-color: #f6bc10;
      overflow: hidden;
      position: fixed;
      top: 0;
      width: 100%;
      z-index: 100;
      padding: 0.75rem;
      display: flex;
      align-items: center;
      border-bottom: 2rem solid black;
    }
  
    .navbar img {
      height: auto;
      max-height: 4rem;
      width: auto;
      margin-right: 1rem;
    }
</style>
  
  <div class="navbar">
    <a href="https://www.kangan.edu.au/campus/cremorne/creative-digital-skills-campus">
      <img id="kangLogo" src={kangLogoUrl} alt="Kangan Logo" />
    </a>
    <a href="https://tafe.educationapps.vic.gov.au/s/">
    <img id="vicLogo" src={vicLogoUrl} alt="Tafe Victoria Logo">
    </a>
  </div>