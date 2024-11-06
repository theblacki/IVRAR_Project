+++
date = '2024-11-06T11:19:40+01:00'
draft = false
title = 'Week1'
+++

# Website Setup with HUGO
HUGO is used to create and publish this website for the project documentation. It was, however, the first time I created a website, as well as used HUGO.
For that reason, the process experience shall be documented here.

## The installation
The installation of HUGO itself went pretty straight forward. Using the documentation on the [HUGO website](https://gohugo.io/getting-started/installing/ "HUGO installation documentation"), getting HUGO to work and creating my first post was done within an hour.

Merely the existence of the extended and extended/deploy versions and their necessity were unclear to me, but installing the base version worked fine for me.

For the theme, I decided on [PaperMod](https://github.com/adityatelange/hugo-PaperMod/ "PaperMod Repository"), simply because it was a blog theme visually appealing to me.

## The Deployment
Actual problems only started cropping up when I tried hosting the site on Github via automatic deployment.

I tried following the referenced [Deployment Guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/ "HUGO Github Deployment Guide") of HUGO, which had it's own stumbling blocks, like not mentioning that the repository has to be public for the pages feature to be available and should be created as such, or not mentioning the actual HUGO website in the workflow.
Should the site be pre-existant, created only afterwards, or does that not matter?

Having already created the site and adding some Git shenanigans made this step take longer than what would've been necessary, but in the end, everything worked out all right and the site ran without problems.

The actual weirdness started only after returning to the slides to continue the setup, when I was confronted with further steps for the deployment. The deployment, which I had just finished?!
Are the slides for an older version of the Guide/HUGO, or are they necessary for something outside of the deployment?

The link (same as above) on the slides does not contain any information on making the repository remote or configuring any kind of access via SSH. The [GitHub documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/managing-deploy-keys "Managing Deploy Keys - Github Documentation") closest to that which I found mentioned deploy scripts, so since those seem to work on my part, I decided against going through any of the additional steps.
That decision was reinforced when I tried adding the **"publishDir: docs"** line to the *hugo.yaml* file and seeing that the site layout was destroyed afterwards. On the website, for some reason, even the post that was still on draft was visible - though as jumbled as the rest.

One thing to be mentioned is, that using the *config.toml* file is outdated and the HUGO documentation itself mentions that users should try to migrate to hugo.xy instead. I had no problems with that, though, since I started by only using the official documentation.

## My first post
I finally tried adding some stuff to my new page, most of which worked splendidly. Only outlier being images, which were already marked as prone to bringing trouble.

I tested via creating a screenshot of the website and including it within:

![img test text](https://theblacki.github.io/IVRAR_Project/static/img/test.png "Title img Text")

I tried adding the image under *.\static\img\* and, following the advice on the slide, later *.\static\img\firstpostname*, and referencing the image itself via https://theblacki.github.io/IVRAR_Project/static/img/test.png, as well as including the post name subfolder later, but to no avail.

For that reason, I included the previously skipped *baseURL* configuration, setting it to https://theblacki.github.io/IVRAR_Project, which fortunately did not destroy the site's format, but also did not help with the image not being shown. Including the *canonifyURLs = true* configuration unfortunaltely also jumbles the page formatting up completely.

<!---
http://localhost:1313/IVRAR_Project/posts/week1/
### H3
[inline link with title](https://www.google.com "Google's Homepage")
#### H4
some text, maybe *italic*, maybe **bold**?
```csharp
string test = "toll";
```
-->