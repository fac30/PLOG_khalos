## Guidance
Answer the following questions considering the learning outcomes for
- [Week 04](https://learn.foundersandcoders.com/course/syllabus/developer/week04-project03-frontend/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Week 4:
This week has been intence because we were a little behind the other teams in terms backed, so on Monday during my free time I completed the logic and implementation of the 2 APIs with our quiz, although as previously mentioned because our game is not just a game, but also a quiz making game, the external APIs play a very little role, the biggest role is taking by the fact we are giving the user the ability to make its own quiz and play it and let others play it.

I created some tests to check if the APIs were being implemented, and it was succesfull:
```ts
// Test route to fetch Giphy GIF based on percentage
router.get('/test-giphy', async (req, res) => {
  const { score } = req.query; // Expect score as a query parameter

  // Convert score to a number
  const numericScore = parseFloat(score as string);

  if (isNaN(numericScore) || numericScore < 0 || numericScore > 100) {
    return res.status(400).json({ error: 'Invalid score. Please provide a score between 0 and 100.' });
  }

  try {
    // Call the service to get the appropriate GIF based on the score
    const gifUrl = await getGiphyByScore(numericScore);

    res.json({
      success: true,
      score: numericScore,
      gifUrl,
    });
  } catch (error) {
    console.error('Error fetching GIF:', error);
    res.status(500).json({ error: 'Failed to fetch GIF' });
  }
});
// end of test
```

To explain this, we are using Giphy api to send a meme at the end of the quiz, once the results appears. If you managed to hit 100% correct questions you will get a very positive GIF, going down each 10% where you will get the saddest, you failed, but still funny GIF.

I used percentages because our users can set how many questions long they want the quiz to be, from 5 up to  like 50.

As a good piano music lover I implemented Spotify to play a song in the background, the user can mute it and unmute it whenever they wish. The playlist selected are piano compositions or iconic movies soundtracks, here is a list of the playlist, these could always be changed by a future dev:
```ts
const backgroundPlaylists = [
  '37i9dQZF1DWWEJlAGA9gs0', // Classical Essentials
  '37i9dQZF1DWTTQ4F9HvbHV', // Ludovico Einaudi Essentials
  '37i9dQZF1DWV0gynK7G6pD', // Classical Focus
  '37i9dQZF1DWXmDxoFybV8T', // Hans Zimmer Soundtracks
  '37i9dQZF1DX7FVBLcFaYHs', // Movie Soundtracks
];
```
Going back to the front-end we started with FIGMA, I love this tool! The videos in Resources were very good and Itzy already had some experience.
When you create the geometrical objects in FIGMA, you kinda understand what components you need, which ones can be re-used, which ones must be their own thing and so on. This really helped us divide the components needed.

Once we had our components ready, we create a folder structure, main folder called "components" and another folder called "pages" which is where we create the Home Page, the Quiz Page or the Quiz Creation Page. 

Itzy and Marika where working on the Quiz Page, which uses the data we already have to display a quiz and let the user play, ad eventually ends in the Result Page where you can check your score, you get the GIF from Giphy, and stretch story you can see the leaderboard.

I worked in the other side of the project, the Quiz Creation part in its entirety. To do so I needed to create a few Input components and Dropdown componends and add some features.

I was struggling with the sanitize part, but I managed to make it a part of our front-end input areas, I will share this later in the section #2 which is things you struggled with.

The first thing I created was the Home Page, the Logo component, I created a logo with an online AI tool, and added 2 buttons under the title that takes you either to play the quizzes we already have or create your own quiz. From there I then created the "InputPage.tsx" which is the page the user sees when creating its own game.

It is composed of a few components:
- Navbar component: This includes a label ("Make your quiz"), on the left of the label there is an arrow, if clicked it takes you back one page, in this case it would take the user back to the Home page. On the right there is a volume up or mute icon which plays the background music or mutes it.
- After the navbar we have all the input elments, starting from the title ("Name of the quiz"):
```tsx
  <TextInput
  placeholder="Enter quiz title"
  label="Name of the quiz"
  value={quizTitle}
  onChange={(value) => setQuizTitle(value)} // Update quiz title state
  isError={!quizTitle && errorMessage ? true : false}
  />
```
All of our inputs have a placeholder in grey font color, to make the user understand what to type in these spaces. After typing their title or in the next inputs they have to type description of the quiz or the questions and answers, the color of the font inside these spaces becomes black, to make the user understand visually that we registered their inputs. This is what `onChange={(value) => setQuizTitle(value)}` is doing.

I implemented some error handling and requirements for our users which you can see in the line `isError={!quizTitle && errorMessage ? true : false}` which works as such: to create a quiz the user must: name the quiz, add a description, select a category, select a difficulty level, create at least 5 q&a, each questions must be unique, within each single q&a block the answers must all be different, also only one can be correct. 

If one of these requirements is not followed, the missing areas will be highlithed with an error message in red colour explaining the user what to do, in this example of the title, if the user was to try and submit the new quiz, but forgot the title, upon pressing the Submit button at the end of the page, a red message would appear next to the button saying "there are requirements to fulfill, scroll up to see the missing info", and when the user scrolls up the title as an example will have a message in red saying "Each quizzes must have a Title".

- Quiz Description component:
```tsx
<TextArea
  placeholder="Enter a description here"
  label="Add a brief description"
  value={quizDescription}
  onChange={(value) => setQuizDescription(value)} // Update quiz description state
  isError={!quizDescription && errorMessage ? true : false}
/>
```
- Category of the quiz:
```tsx
<CategoryDropdown
  onChange={setCategory} 
  isError={category === 'Select Category' && errorMessage ? true : false}
/>
```
- Difficulty dropdown:
```tsx
<DifficultyDropdown
  onChange={setDifficulty} 
  isError={difficulty === 'Select Difficulty' && errorMessage ? true : false}
/>
```
- Q&A blocks:
```tsx
{questions.map((q, index) => (
  <div key={index} className="mb-4">
    <TextInput
      label={`Question ${index + 1}`}
      placeholder="Type the question here"
      value={q.question}
      onChange={(value) => handleInputChange(index, 'question', value)}
      isError={checkDuplicateQuestion(q.question, index)}
    />
    <TextInput
      label="Correct Answer"
      placeholder="Type the correct answer here"
      value={q.correctAnswer}
      onChange={(value) => handleInputChange(index, 'correctAnswer', value)}
      isError={q.correctAnswer === '' || q.wrongAnswers.includes(q.correctAnswer)}
    />
    {q.wrongAnswers.map((wrongAnswer, i) => (
      <TextInput
        key={i}
        label={`Wrong Answer ${i + 1}`}
        placeholder="Type the wrong answer here"
        value={wrongAnswer}
        onChange={(value) => handleInputChange(index, `wrong_${i}`, value)}
        isError={q.wrongAnswers.includes(wrongAnswer) || wrongAnswer === q.correctAnswer}
      />
    ))}
  </div>
))}
```
- 2 final buttons, one is "Add new questions" which creates one more Q&A block, and the Sumbit button which displays a popup centered on the screen both vertically and horizontally saying "Thank you for creating a new quiz" and 2 buttons, one saying "Go to Home page" and one saying "explore quizzes" where you would find your newly created quiz as well as the ones already in the system.

Some useful code, how to create the red error message at each line and with descriptive info when requirements are not met:
```tsx
// Validation Logic
if (!quizTitle || !quizDescription || category === 'Select Category' || difficulty === 'Select Difficulty') {
  setErrorMessage('Please fill in all fields: quiz title, description, category, and difficulty.');
  return false;
}

// Duplicate Questions Check
if (questionSet.has(q.question)) {
  setErrorMessage('Each question must be unique.');
  return false;
}

// Summary error message
{errorMessage && <div className="text-red-500 text-center mt-4">Please review and fix the errors above.</div>}
```

Popul appearing after Submittin succesfully your new quiz:
```tsx
{showModal && (
  <Modal
    message="Thank you for creating your quiz!"
    onClose={() => setShowModal(false)}  // this is at the end of the pop up in case you want to close it
    onHome={navigateHome} // takes the user to homepage
    onExplore={navigateExplore} // takes user to explore quizzes
/>
)}
```

 ### 2. Struggles:
Understanding validate & sanitize wasn't easy, but I can see the importance of it, especially our quiz being so different from the other teams where our user can literaly create a new quiz, accessing our database almost fully. I implemented the sanitize in our Input comments, this is an example:
```tsx
const sanitizeInput = (value: string) => {
  return value
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')
    .replace(/&/g, '&amp;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#39;');
};

const TextArea: React.FC<TextAreaProps> = ({ label, placeholder, onChange }) => {
  const [inputValue, setInputValue] = useState<string>('');

  const handleChange = (event: React.ChangeEvent<HTMLTextAreaElement>) => {
    const value = event.target.value;
    const sanitizedValue = sanitizeInput(value);
    setInputValue(sanitizedValue);
    onChange(sanitizedValue);
  };
```
I learned many other things this week, more TypeScript on Execute Program, more notes taken on my Obsidian, Levi showed me some of his work, the basics of React etc...

## Feedback (For CF's)
> [**Course Facilitator name**]

Alexander

> [*What went well*]

Very detailed progress log, thanks for sharing. Snippets are good quality and looks like you got all the important learning for this week 

> [*Even better if*]

You could be a bit more concise, there is no need to mention the specifics of your group dynamics. Consider this log more like a resource or a repository where you keep track of important learnings and code examples of those. Almost like a cheatsheet.
