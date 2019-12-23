+++
categories = ["tutorial"]
date = "2019-12-21"
description = "A beginner-friendly guide to making a static website."
title = "Making a Website"
type = "post"

+++

To make this website, I used the Hugo static site generator and am hosting my site on GitHub pages. What does that mean?

GitHub Pages allows you to host a static site, either on the github.io domain or a custom domain, and is free if you have a GitHub account. I created a GitHub user/organization page, which means that my site is available at \<username>.github.io. The steps are outlined in the [documentation](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site) for GitHub pages. Then, I followed these [directions](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site) to configure my custom domain to redirect from heraaali.github.io to heraaali.com.

So, you can host a static site for free, but how to make that static site? One way is to use a static site generator. I chose to go with Hugo because it is fast, has beginner-friendly documentation, and has lots of [themes](https://themes.gohugo.io/) to choose from. I followed the [directions](https://gohugo.io/getting-started/quick-start/) on the Quick Start page, and used the Hugo Future Imperfect Slim theme. 

To make posts with Hugo, you create files in markdown with the correct metadata, and run Hugo to generate your static site. I have definitely been tripped up by having the incorrect metadata, meaning my posts wouldn't show up on my homepage!

Finally, I followed the steps on the Hugo site for [hosting on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/).

As you can see, a lot of the work was following the right directions in the right order :) 


In summary,

1. Create a GitHub user/organization page.
2. (optional) Redirect to a custom domain name of your choosing.
3. Use a static site generator to create a local version of your website. Customize the css, make posts, etc. until you are happy with how it looks.
4. Deploy your website to your \<username>.github.io repo and watch your site go live!


