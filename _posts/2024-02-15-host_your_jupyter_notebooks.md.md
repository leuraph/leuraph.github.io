---
layout: post
title: Hosting your Jupyter Notebooks
date: 2024-02-15 10:00:00+0100
description: A cute way of (interactively) hosting your Jupyter Notebooks
tags: notes
categories: labbook
related_posts: false
---

In case you want to host a Jupyter Notebook in an interactive way,
i.e. by embedding a hosted notebook on any existing website
(e.g. this website hosted on github pages),
you can do this easily in the following way.

- Follow the instructions found on the [official doc](https://jupyterlite.readthedocs.io/en/latest/quickstart/deploy.html) to deploy and host your own JupyterLite website on github pages.
- Add (commit and push) any notebook you want to host to your repo.
- To embed a live environment on your website, you can follow [this guide](https://jupyterlite.readthedocs.io/en/latest/quickstart/embed-repl.html).
- To embed the Notebook in your existing website, simply include the following code snippet.
  ```html
  <iframe
    src="https://your_username.github.io/your-repo/notebooks/index.html?path=path/to/notebook.ipynb"
    width="100%"
    height="500px"
  >
  </iframe>
  ```
  In my case, the result looks like this.

<iframe
  src="https://leuraph.github.io/jupyter-notebooks/notebooks/index.html?path=p5.ipynb"
  width="100%"
  height="500px"
>
</iframe>