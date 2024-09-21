## Guidance
Answer the following questions considering the learning outcomes for
- [Week 02](https://learn.foundersandcoders.com/course/syllabus/developer/week02-project02-chatbot/learning-outcomes/)

Make sure to record evidence of your processes. You can use code snippets, screenshots or any other material to support your answers.

Do not fill in the feedback section. The Founders and Coders team will update this with feedback on your progress.

## Assessment
 ### 1. Show evidence of some of the learning outcomes you have achieved this week.
> This week was great! I learned more about backend, working with APIs, testing my code in different ways.
> 
> The one thing I am the most proud of is being able to research about a topic I have never studied before and succesfully completing the project with my team.
> 
> I found very interesting the testing part, and I can see why it is good practice to authomate it.
> 
> Here you can see some testing code I wrote to check if the server was communicating with the OpenAI:
>
```
const dotenv = require('dotenv').config();

const serverBridge = require('./app');

module.exports = {
  // Simulates Discord messages and the response function
  listenToMessages: async (handleMessage) => {
    const testMessage = ["What is the capital of France?",
      "What is its population?",
      "What are its main attractions"
    ]; // Example test message

    // Simulate a reply function

    const reply = (chatResponse) => {
      // console.log(typeof reply());
      console.log('Replying with:', chatResponse);
    }

    // Call the handler function with the test message and reply function
    for (message of testMessage) {
      await handleMessage(message, reply);
    }
  }
};
```


 ### 2. Show an example of some of the learning outcomes you have struggled with and/or would like to re-visit.
> I would like to revisit async await in general and practice more JavaScript Concurrency. I did complete the course on Execute Program and I started with the TypeScript Basics course. 
>
> I believe FAC has access to my Execute Program stats, please let me know if you need further evidence, I can post screenshots of the topics I strugged with the most, but they were within the course.
>
> I am reviewing code almost every day, this should help make me understand better all the concepts I have learned this week.

## Feedback (For CF's)
> [**Course Facilitator name**]  
> [*What went well*]  
> [*Even better if*]
