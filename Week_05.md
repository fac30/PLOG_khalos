## Guidance
Answer the following questions considering the learning outcomes for
- [Week 05](https://learn.foundersandcoders.com/course/syllabus/developer/week05-project03-test-deploy/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
# Weekly Development Summary

This week, I focused on multiple aspects of the quiz application, including API integration, UI/UX improvements, state management in React, and responsive design. Below is a summary of what I learned and worked on, along with code snippets to illustrate the key concepts.

## What I Learned and Coded

### 1. **Navbar with Dynamic Titles**

One of the first tasks was to create a dynamic `Navbar` that changes its title based on the quiz the user selects. This required extracting quiz titles from an API and passing the data down as props to the `Navbar` component. The key challenge was ensuring the navbar always displayed the correct title, even when navigating between different quizzes:
```tsx
import React from 'react';
import { useLocation } from 'react-router-dom';

type NavProps = { title: string };

const Navbar: React.FC<NavProps> = () => {
  const location = useLocation();
  const quizTitle = location.state?.quizName || "Loading...";

  return (
    <nav className="navbar flex justify-between items-center">
      <h2>{quizTitle}</h2>
    </nav>
  );
};

export default Navbar;
```

A major part of UI/UX development was ensuring that the components were laid out in a user-friendly manner. One challenge was positioning elements like the question counter on the top-right corner while keeping the question text centered. I used flex and justify-between properties in Tailwind CSS to achieve this layout:
```tsx
<div className="flex justify-between items-start">
  <h2 className="text-xl">{question.text}</h2>
  <span className="bg-gray-200 text-sm px-4 py-2 rounded-md">
    {index + 1}/{totalQuestions}
  </span>
</div>
```
Using utilities from Tailwind CSS made it easier to create responsive and well-positioned layouts.
Jason, Jack and Max were impressed with how clean the graphics of our project are, this is thanks to Tailwind, and the base Figma work Itzi made.
This is the first time I develop a project for mobile first.

 ### 2. Show an example of some of the learning outcomes you have struggled with and/or would like to re-visit.
I struggled with accessibility. I was not sure how to implement the best accessibility practices into the project without sacrificing the visuals. Our team tried to keep the aestethics as clean as possible, having the text set to BLACK and the background to WHITE really helped colour contrast, which is why we kept this colour palette.

One of my colleagues de-activated the Focus option because it distracted their coding, which we should have re-activated for the final project and we didn't. I am also responsible for not remembering that. This taught me that if in the future some of the developers in my team are disactivating Focus or other functionalities needed for the final user during the developement, I should take notes to remember to re-activate them at the end of the developement.

The button to navigate back to the previous page in the Navbar is another example of me not being sure how to make it more accessible. I edited it to look and behave like a button, but thanks to the Thursday talk I now understand how inaccessible it is, and how I should implement it in future projects.

## Feedback (For CF's)
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
