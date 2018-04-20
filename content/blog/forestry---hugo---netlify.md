+++
date = "2018-04-20T01:17:47+00:00"
title = "Forestry + Hugo + Netlify"

+++
Just when I thought my publishing setup was finalized, I stumbled across [Forestry](https://forestry.io). Forestry appears to solve my GUI wishlist all at once. GUI for Hugo? Check. Well designed for clients? Check. Can be mapped to my URL? Check. Well supported and documented? Check.

<!--more-->

![](/uploads/2018/04/20/Screen Shot 2018-04-19 at 9.25.50 PM.png)

My previous workflow is still relevant for quick changes I want to make, and for modifying the sites design or theme. But, when I'm just writing new posts, I'll go through the Forestry GUI. Enabling Forestry slightly changed my backend setup. Here is how it works now:

1. I linked Forestry to my Github account containing the Hugo project.
2. I made a new, empty Github pages repo.
3. In Forestry settings, I selected the Github pages repo as a publish target. This means when I publish, Forestry will run the `Hugo` command and copy the output to the repo.
4. I now sync the Github pages repo to Netlify instead of the original Hugo repo.
5. On my local machine, pull down the master branch and run `dat .` as I did before to sync the dat archive.

It's worth noting that you can just use GitHub pages to host your site. I stayed with Netlify for the free SSL, to try something new, and because it appears to clear cache faster. 

Also, as a one time setup, [link the Forestry admin panel to your sites URL](https://forestry.io/docs/editing/remote-admin/).