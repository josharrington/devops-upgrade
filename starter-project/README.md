# Starter Project

Because a DevOps Engineer is not an entry-level position, you need to be able to demonstrate your skills to employers to make it in this field. You will need to show off your skills in systems management, networking, development, and release management. The projects in this repo will give you some foundations to build on and let you build a portfolio to exhibit your new-found skillset.

# Part 0

1. Get a Github account. You need somewhere to save your code and to show it off! If you've never used git beofre,
2. Get a good code editor. If you don't already have a favorite, VS Code is a good choice and works on all platforms.
3. Set aside some time several times per week to work on this. Don't let it stagnate.
4. Any computer you have access to will be able to perform all these steps. You do not need special equipment.

# Part 1 - Build Something

If you are going to support a development organization, you need to understand what it takes to build software. This will not get you the full exposure of a software engineering position but will help you get familiar with softare development in general.

You will need to build a web service that performs some task. This can be anything you want! I recommend building something relevant to your interests. Choose any language or framework you feel most comfortable with.

Go as far and wide as you want for this service. Keep it as just a simple HTTP endpoint or go big and build a nice HTML/CSS/JS UI around it too! Bonus points if you separate the two into separate services.

Your service should have the following basic parts, however:

1. Should talk HTTP. This ensures the service you build will be ready for the next parts. It also let's anybody interact with it!
2. Should be stored in a Github repo.
3. Should follow the principals of the [twelve factor app](https://12factor.net/). Importantly, never commit credentials to your repo!

If you are stuck on what to build, here are a few project ideas to get you started. Feel free to modify them as you wish. Or build multiple to start getting comfortable!

1. Warm up: A basic HTTP service that performs basic arithmetic. The service should accept a POST with two or more numbers and perform an operation against them as specified by the user.
2. Build a basic blog engine. The website will consist of one page where blog posts are displayed and another where blog posts are submitted. The blog contents will be stored in a database.
3. Build an image hosting website. The website will allow users to upload an image that will then be hosted by your website, similar to Imgur. You should process the images so that you have a thumbnail, the original image, and an image with a watermark on top of it. All of these should be available to the user after uploading. The user should also have a way to delete the image later.

Ensure the project is well documented and includes a README to introduce readers to it and explain how to run it.

# Part 2 - Deploy It

So you have a web service you've built on your own. Great! Now you need to deploy it.

TODO

# Part 3 - Continuous Integration and Deployment

TODO

# How do I stand out?

Now that you have a service that is deployed and showcased, how do you differentiate yourself from the other people doing the same?

- Add unit tests and/or to your code
- Make your website look pretty.
- TODO