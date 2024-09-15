## Guidance

Answer the following questions considering the learning outcomes for

- [Week 01](https://learn.foundersandcoders.com/course/syllabus/developer/week01-project01-basics/learning-outcomes/)
  
Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

Assessment
1. Show evidence of some of the learning outcomes you have achieved this week.

Learning outcome:

a. How GitHub works: (thanks to the project01 which guided us step by step) how to clone a main repository and create a new one to implement new changes and feautures. How to then save the new features and merge them back into the main.

b. Team management: thanks to Jason and Danielle's incredible team spirit. I understood better how to manage a project, divide tasks, set some priorities and so on.

c. I had a good read about CSS and HTML standards, as well as how important accessibility is. (Links in Resources area).

d. I studied the Execture Program about JavaScript Concurrency (currently at 61% of the course). I also watched the YouTube videos about the same topic, linked in the resources section of Week 1.

e. I learned how to use HackMD and gained more confidence presenting projects in public.

My evidence:

a. GitHub project (link): [https://github.com/orgs/fac30/projects/15/views/1?layout=board](https://github.com/orgs/fac30/projects/15)

b. The JavaScript to change colour variables of the CSS file (in :root): 

// COLOUR SWITCHER

document.getElementById('planetsNav').addEventListener('change', function(event) {
  const planetName = event.target.value.toLowerCase();
  
  // Get the selected planet's data (e.g., jupiter, mars)
  
  const planet = window[planetName]; // Assuming you have them in global scope
  const description = planet.getDescription();

  // Update page content
  
  document.getElementById('planetName').innerHTML = planet.name;
  document.getElementById('infoLeft').innerHTML = description.column1;
  document.getElementById('infoRight').innerHTML = description.column2;

  // Update theme colors
  
  document.documentElement.style.setProperty('--color-1', planet.colors.color1);
  document.documentElement.style.setProperty('--color-2', planet.colors.color2);
  document.documentElement.style.setProperty('--color-3', planet.colors.color3);

  // Update planet img
  
  const image = document.getElementById('planetImage');
  image.src = planet.image;
});

// We started from the idea of implementing a switching themes, but then added info about each planets and changed the image.


3. Show an example of some of the learning outcomes you have struggled with and/or would like to re-visit.

Learning outcome:

I want to imporove the way a project is presented, the structure of CSS, HTML, JS, how to organise files, naming conventions and other standards. I have read some articles linked in Resources to improve my understanding on this topic, I still need to practice and learn more on this topic. This is also my role within the team, I will do my best to achieve a positive outcome.

Feedback (For CF's)
[Course Facilitator name]
[What went well]
[Even better if]
