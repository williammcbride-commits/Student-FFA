<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FFA Animal & Agriculture Info</title>
  <link href="https://fonts.googleapis.com/css2?family=Caveat&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Caveat', cursive;
      background-color: #eaf2e3; /* light green background */
      color: #333;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #004d00; /* dark green */
      color: #ffd700; /* gold */
      padding: 20px;
      text-align: center;
    }
    header h1 {
      margin: 0;
    }
    nav {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 15px;
      padding: 10px;
      background-color: #006600;
    }
    nav a {
      color: #ffd700;
      text-decoration: none;
      font-weight: bold;
    }
    nav a:hover {
      text-decoration: underline;
    }
    main {
      padding: 20px;
      max-width: 1200px;
      margin: auto;
    }
    section {
      margin-bottom: 40px;
    }
    section h2 {
      color: #004d00;
      border-bottom: 2px solid #ffd700;
      padding-bottom: 5px;
    }
    ul {
      list-style-type: none;
      padding: 0;
    }
    ul li {
      margin: 10px 0;
    }
    ul li a {
      color: #006600;
      text-decoration: none;
    }
    ul li a:hover {
      text-decoration: underline;
    }
    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin-bottom: 20px;
      font-size: 1rem;
    }
    footer {
      background-color: #004d00;
      color: #ffd700;
      text-align: center;
      padding: 15px;
    }
  </style>
</head>
<body>

  <header>
    <h1>FFA Animal & Agriculture Info</h1>
    <p>All the latest FFA news, events, and animal programs in one place</p>
  </header>

  <nav>
    <a href="#animals">Animals & CDEs</a>
    <a href="#stories">Member Stories</a>
    <a href="#awards">Awards & Competitions</a>
    <a href="#events">Events & Conferences</a>
    <a href="#advocacy">Advocacy & Careers</a>
  </nav>

  <main>
    <input type="text" id="searchInput" placeholder="Search by keyword, animal, or year..." onkeyup="searchArticles()">

    <!-- Animals Section -->
    <section id="animals">
      <h2>Animals & CDEs</h2>
      <ul id="animalList">
        <li><a href="https://www.ffa.org/participate/cdes/veterinary-science/" target="_blank">Veterinary Science CDE</a></li>
        <li><a href="https://www.ffa.org/participate/poultry/" target="_blank">Poultry Evaluation CDE</a></li>
        <li><a href="https://www.ffa.org/participate/cdes/meats-evaluation-and-technology/" target="_blank">Meats Evaluation & Technology CDE</a></li>
        <li><a href="https://www.ffa.org/participate/cdes/livestock-evaluation/" target="_blank">Livestock Evaluation CDE</a></li>
        <li><a href="https://www.ffa.org/participate/cdes/horse-evaluation/" target="_blank">Horse Evaluation CDE</a></li>
        <li><a href="https://www.ffa.org/participate/cdes/dairy-cattle-evaluation-management/" target="_blank">Dairy Cattle Evaluation & Management CDE</a></li>
      </ul>
    </section>

    <!-- Member Stories Section -->
    <section id="stories">
      <h2>Member Success Stories</h2>
      <ul>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/giving-students-goat-opportunities/" target="_blank">Nevaeh Locklear - Raising & Showing Goats</a></li>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/raise-a-life-change-a-life/" target="_blank">Aydin Anbarci - Training a Service Dog</a></li>
        <li><a href="https://www.ffa.org/sae/equine-sae/" target="_blank">Roselynn Orr - Equine Apps</a></li>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/chasing-dreams-with-an-sae-katies-car-freshies/" target="_blank">Katie Aubert - Car Freshies Business</a></li>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/ffa-experience-new-opportunities/" target="_blank">Casey Spencer - Animal Passion Leads to Opportunities</a></li>
      </ul>
    </section>

    <!-- Awards Section -->
    <section id="awards">
      <h2>Awards & Competitions</h2>
      <ul>
        <li><a href="https://www.ffa.org/american-star-awards/meet-the-finalists-2023-american-star-farmer/" target="_blank">2023 American Star Farmer Finalists</a></li>
        <li><a href="https://www.ffa.org/american-star-awards/meet-the-finalists-2023-american-star-in-agriscience/" target="_blank">2023 American Star in Agriscience Finalists</a></li>
        <li><a href="https://www.ffa.org/press-releases/national-ffa-announces-2020-national-agricultural-proficiency-winners/" target="_blank">2020 National Agricultural Proficiency Winners</a></li>
        <li><a href="https://www.ffa.org/press-releases/national-ffa-announces-winners-for-national-ffa-agriscience-fair/" target="_blank">2020 National FFA Agriscience Fair Winners</a></li>
      </ul>
    </section>

    <!-- Events Section -->
    <section id="events">
      <h2>Events & Conferences</h2>
      <ul>
        <li><a href="https://www.ffa.org/press-releases/national-ffa-members-head-to-washington-d-c-for-washington-leadership-conference/" target="_blank">Washington Leadership Conference</a></li>
        <li><a href="https://www.ffa.org/participate/next-generation-conference/" target="_blank">Next Gen Conference - Animal Systems Pathway</a></li>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/aggies-camp-inspires-youth-through-hands-on-lessons/" target="_blank">Aggie's Camp - Hands-on Animal Lessons</a></li>
        <li><a href="https://www.ffa.org/ffa-in-the-usa/keeping-students-safe-on-the-farm/" target="_blank">Farm Safety Days</a></li>
      </ul>
    </section>

    <!-- Advocacy & Careers Section -->
    <section id="advocacy">
      <h2>Advocacy & Careers</h2>
      <ul>
        <li><a href="https://www.ffa.org/agricultural-education/" target="_blank">Agricultural Education</a></li>
        <li><a href="https://www.ffa.org/start-an-ffa-chapter/" target="_blank">Start an FFA Chapter</a></li>
        <li><a href="https://www.ffa.org/ag-101/talking-points-speakag/" target="_blank">FFA Advocacy Talking Points</a></li>
        <li><a href="https://www.ffa.org/career-pathways/5-emerging-steam-careers-in-agriculture/" target="_blank">Emerging STEAM Careers in Agriculture</a></li>
      </ul>
    </section>
  </main>

  <footer>
    &copy; 2026 FFA Animal & Agriculture Info | All Rights Reserved
  </footer>

  <script>
    function searchArticles() {
      let input = document.getElementById('searchInput').value.toLowerCase();
      let lists = document.querySelectorAll('section ul li');
      lists.forEach(item => {
        if(item.textContent.toLowerCase().includes(input)) {
          item.style.display = '';
        } else {
          item.style.display = 'none';
        }
      });
    }
  </script>

</body>
</html>
