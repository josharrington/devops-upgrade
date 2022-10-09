# Part 1 - Build Something

If you are going to support a development organization, you need to understand what it takes to build software. This will not get you the full exposure of a software engineering position but will help you get familiar with softare development in general.

You will need to build a web service that performs some task. This can be anything you want! I recommend building something relevant to your interests. Choose any language or framework you feel most comfortable with.

Go as far and wide as you want for this service. Keep it as just a simple HTTP endpoint or go big and build a nice HTML/CSS/JS UI around it too! Bonus points if you separate the two into separate services.

Your service should have the following basic parts, however:

1. Should talk HTTP. This ensures the service you build will be ready for the next parts. It also let's anybody interact with it!
2. Should be stored in a Github repo.
3. Should follow the principals of the [twelve factor app](https://12factor.net/). Importantly, never commit credentials to your repo!
4. Intentionally leave out one or two features you would like to implement. We'll follow up on those later. Create issues in Github to track the progress of those missing features.

If you are stuck on what to build, here are a few project ideas to get you started. Feel free to modify them as you wish. Or build multiple to start getting comfortable!

1. Warm up: A basic HTTP service that performs basic arithmetic. The service should accept a POST with two or more numbers and perform an operation against them as specified by the user.
2. Build a basic blog engine. The website will consist of one page where blog posts are displayed and another where blog posts are submitted. The blog contents will be stored in a database.
3. Build an image hosting website. The website will allow users to upload an image that will then be hosted by your website, similar to Imgur. You should process the images so that you have a thumbnail, the original image, and an image with a watermark on top of it. All of these should be available to the user after uploading. The user should also have a way to delete the image later.

Not sure which language or framework to choose? Use Python and Flask. [See here for a tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).

Ensure the project is well documented and includes a README to introduce readers to it and explains how to run it.

### Acceptance criteria
1. Your service exposes an HTTP endpoint and performs some logic based on user input.
2. Your application code is saved in a Github repo.
3. Includes a README.md at the root level with screenshots and instructions on how to build and run it.
4. Follows the principles in [The Twelve Factor App](https://12factor.net).

---

[Continue to Part 2](part2.md)