---
title: Deploying to Firebase Hosting
---

In this guide, you will learn how to deploy your Gatsby site to Firebase Hosting.

[Firebase Hosting](https://firebase.google.com/docs/hosting) is a free web content hosting platform for developers. With a single command, you can quickly deploy web apps and serve both static and dynamic content to a global CDN (content delivery network).

## Pre-requisites

1. Make sure you have:

   - installed [Node.js](https://nodejs.org/en/download/) on your local machine.
   - a [Firebase Account](https://console.firebase.google.com).
   - created a [Firebase Project](https://firebase.google.com/docs/web/setup#create-firebase-project).

1. This guide assumes that you already have a Gatsby project on your local machine.

## Deployment

1. Install the Firebase CLI with `npm` by running the following command:

   ```shell
   npm install -g firebase-tools
   ```

1. Sign into Firebase using your Google account by running the following command:

   ```shell
   firebase login
   ```

   You can test if the CLI is correctly installed by running `firebase projects:list`, which should show you a list of your Firebase Projects.

1. Navigate into your gatsby project directory and setup firebase:

   ```shell
   firebase init
   ```

   This command will prompt you to:

   - select the Firebase products you wish to setup. Be sure to select **Firebase Hosting**.
   - select the Firebase Project you wish to use or create a new one, if you haven't done it previously.

   When prompted to select your public directory, press <kbd>enter</kbd>. It will default to `public`, which is also Gatsby's default public directory.

1. Prepare your site for deployment by running `gatsby build`. This generates a publishable version of your site in the `public` folder.

1. Deploy your site by running the following command:

   ```shell
   firebase deploy
   ```

All done! Once the deployment concludes, you can access your website using `firebaseProjectId.firebaseapp.com` or `firebaseProjectId.web.app`.

Check the [Firebase Docs](https://firebase.google.com/docs/hosting/full-config) for information about how to customize your deployment further. Remember that each time you wish to redeploy your site, you will need to rerun `gatsby build` first.

## References:

- [Firebase CLI Reference](https://firebase.google.com/docs/cli)
- [Get Started with Firebase Hosting](https://firebase.google.com/docs/hosting/quickstart)
- [Connect a custom domain](https://firebase.google.com/docs/hosting/custom-domain)
