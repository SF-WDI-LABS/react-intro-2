# You Do: A Blog Post

Let's have some practice creating a React component from scratch. How about a blog post?

Change directories back into the main directory where you want to keep your code (outside the hello_world React app directory we've been working on).

Referring to everything we've done up until now, create a new project using create-react-app. If you need to refresh your memory, refer to the Initial Setup section or view the official create-react-app Github repository.

Note: Because `create-react-app` runs on port 3000, you'll have to stop the current `hello_world` app in order to view this new app (generally, hit ctrl + c in the Terminal window in which it's running).
In src/App.js, change the App component to be a Post component.

Note: Normally, it would be good practice to rename the App.js file Post.js or to create a new component file for the Post component entirely. Then it would be obvious which component each file contains. However, don't do this! This is a comment for you to know best practices for the future - in this tutorial, leave the file named App.js. We're just concentrating on making it work for now!

Create a post object in src/index.js that has the following properties:

- title (example value: "Dinosaurs are awesome")
- author (example value: "Stealthy Stegosaurus")
- body (example value: "Check out this body property!")
- comments (example value: ["First!", "Great post", "Hire this author now!"])
- Render a Post component with the information from your post object as its props values. For now, only include one of the comments. You decide how you want to display the title, author, body, and comment, or you can use the screenshot in the Solution section below as inspiration.

**Optional:** adjust the CSS of your index file body to align your text to the center of the document.

### Solution

Here's what the solution might look like:

Solution for Project
https://imgur.com/a/MUb5v

Once you have a solution:

You can check a sample solution here!
