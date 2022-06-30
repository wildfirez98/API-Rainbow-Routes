# API-Rainbow-Routes-with-Typescript
Activity: Getting Started with TypeScript Part 2

You've already learned the basics of setting up a TypeScript project. It would be nice if that were everything, but there's still some more setup situations we need to look at. For this lesson, we'll be looking at how to get TypeScript set up for an Express application. To do this, we'll be revisiting one of your first back-end projects-Rainbow Routes.
Setup
Instructions:

    Click HERE for the link to the repo.
    Fork (not clone) it to your OWN GitHub account.
    Now to clone the repo to your machine, click the green 'Code' button and then copy the URL.
    In a new terminal, or Git Bash, go to where you want to clone the repo.
    Type git clone in the terminal or Git Bash, then a space, then paste the URL you copied from your repo. Example:
    undefined

Hit "Enter" or "Return", whichever is on your keyboard.
Now, in your terminal, change to your repository directory (cd repo name)
Open your repository in Visual Studio Code.
Open terminal in your Visual Studio Code.
In your terminal, run npm install to install the required node_modules.
After the install, run npm start in the terminal.
Do the assignment in Visual Studio Code and stage your changes using the git add -A command.
Make at least one commit by using the git commit -m "write your message here" command. Example:
undefined
Finally, push your changes using the git push command. Example:
undefined

    You should see something like this open in your browser:

undefined
undefined
1) Set Up Your Project

Before getting started, you'll want to stop nodemon from running. Use Control+C to stop nodemon. Don't worry, we'll get nodemon back, but there are some special settings we need in order to get it working with TypeScript. Based on what you learned in the last lesson, set up the project structure to use TypeScript, including

    Update the folder structure and place source .js files into a src folder.
    Convert any .js files to .ts files.
    Add the TypeScript build script to package.json
    Install the TypeScript dependency.
    Add tsconfig.json and configure with necessary settings.

Your file browser should look something like this:
TS file browser
2) Set Up nodemon

In order to set up our project to work with Express, there are a few more steps that we need to take. The first is to get nodemon working with TypeScript.

nodemon will not work by default with TypeScript. In order for it to work, you must install ts-node. Ts-node is an engine and REPL for TypeScript. It will allow us to use TypeScript with nodemon. To install, run npm i -g ts-node Now that ts-node is installed, nodemon will work. By default, nodemon will look for an index.js file in the directory it is called in. Run nodemon src/index.ts to help nodemon find your TypeScript.

You will notice that nodemon crashes. nodemon will only run without TypeScript errors.

Remember: Even if there are errors in your TypeScript, it will still compile. So if nodemon isn't working, you can still run your compile script and then run your index file in Node.js to test if your JS is working despite the TypeScript errors.
3) Add Type Definitions

Look at your index.ts file. If using an editor like VSCode, you'll see that TypeScript is already showing you some changes that should be made. Otherwise, run your build script to see what errors TypeScript is running into.
TypeScript errors

Look at the first error listed for require and notice the hint it's giving us. It's asking us if we need to install type declarations for node. The prompt given for type declarations is almost always accurate. In some rare occasions, type declarations may not yet exist for the package you're working with. We'll cover creating type declarations in a later lesson.

Install the type declarations for node with:
undefined

Once node type declarations are installed, running your build script should show four remaining errors.

The remaining errors all relate to the req and res parameters from Express. This should be a big hint that we also need type declarations for Express. When using TypeScript, most every package you add to your dependencies will also need type declarations. To add type dependencies for Express, run:
undefined

Our issues are not fixed! TypeScript expects us to use the latest features of EcmaScript. This means using import to import Express; otherwise, it won't pull in the type declarations. Update require to import
import express

At this point, it should appear as though we are done. All our errors are resolved, but let's take it a bit further.
4) Type Annotations

When working with a library or framework like Express, it's best to allow TypeScript to use type inference to type parameters and returns specific to the library. However, let's see how we could type our req, res parameters and where else we could add types.

Hovering over function will give a hint.
request response

It appears that we could use the following:
Request Fetch

But doing so actually calls interfaces from the Fetch API rather than Express. So we need to tell TypeScript to use types from Express.
undefined

And since we're not returning anything, we can use void as the return type.

We know that our query parameter is going to be a string, but what if we didn't know what type of data it was going to be? We would use the unknown type.
undefined

Typing myColor as such causes another error. String methods will not work on type unknown
unknown type

To remedy this, we can use type narrowing to narrow the type to string
undefined
5) Bonus

Try further modifying the type of myColor See what happens when you try other types and what errors you receive. What happens if you try to type const app?
