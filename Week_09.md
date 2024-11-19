## Guidance
Answer the following questions considering the learning outcomes for Week 09

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
I completed all Execute Program courses needed by Monday this week!
I learned a bit about .Net, but I worked mainly in the FE using React, TypeScript and Vite. 
The most interesting thing is that I made my firt dark mode react component to switch themes of our website depending on the user's system preferences.
``` tsx
import { useEffect, useState } from 'react'; // Import hooks from React
import { FaSun, FaMoon } from 'react-icons/fa'; // Import Sun and Moon icons from react-icons library

// This component implements a dark mode toggle functionality
export default function DarkModeToggle() {
  // useState to manage dark mode state, initialized with a function:
  const [isDarkMode, setIsDarkMode] = useState(() => {
    // Check localStorage for the saved theme preference ('dark')
    // If none is saved, use the system preference via matchMedia
    return localStorage.getItem('theme') === 'dark' ||
           (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches);
  });

  // useEffect to update the theme whenever `isDarkMode` changes
  useEffect(() => {
    if (isDarkMode) {
      // Add the 'dark' class to the root HTML element
      document.documentElement.classList.add('dark');
      // Save the dark theme preference in localStorage
      localStorage.setItem('theme', 'dark');
    } else {
      // Remove the 'dark' class from the root HTML element
      document.documentElement.classList.remove('dark');
      // Save the light theme preference in localStorage
      localStorage.setItem('theme', 'light');
    }
  }, [isDarkMode]); // Dependency array: runs whenever `isDarkMode` changes

  // Function to toggle between dark and light modes
  const toggleDarkMode = () => setIsDarkMode(!isDarkMode);

  // Return a button to toggle dark mode
  return (
    <button
      onClick={toggleDarkMode} // On click, call the toggleDarkMode function
      aria-label="Toggle Dark Mode" // Accessibility label for screen readers
      className="bg-electric-yellow dark:bg-dark-charcoal text-midnight-blue dark:text-soft-white p-2 rounded-full shadow-md transition-colors"
      // Tailwind CSS classes for styling:
      // - `bg-electric-yellow` for light mode background, `dark:bg-dark-charcoal` for dark mode background
      // - `text-midnight-blue` for light mode text, `dark:text-soft-white` for dark mode text
      // - Padding (`p-2`), rounded corners (`rounded-full`), shadow (`shadow-md`), and smooth color transitions (`transition-colors`)
    >
      {isDarkMode ? <FaSun size={18} /> : <FaMoon size={18} />}
      {/* Render Sun icon when in dark mode, and Moon icon when in light mode */}
    </button>
  );
}

```

 ### 2. Show an example of some of the learning outcomes you have struggled with and/or would like to re-visit.
.Net in general. I am still doing the basics.

## Feedback (For CF's)
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
