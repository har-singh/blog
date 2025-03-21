---
layout: post
title: Getting Ready for Jekyll Minima Theme on GitHub Pages
date: 2025-03-21 18:36
author: learninghar
comments: true
categories: [blog]
---

I had to recreate my development environment again, so I decided to document the initial setup steps this time for future reference. The starting point is the official Jekyll documentation: [[Jekyll Docs](https://jekyllrb.com/docs/)](https://jekyllrb.com/docs/), but it assumes that Ruby and the `gem` package manager are already installed. Instead of installing packages directly on my machine, I opted to use a Docker container as the development environment.

## Using Docker for Jekyll Development

To use a Docker image while leveraging the repository's code, run the following command:

```sh
sudo docker run -it --name ruby-gem --privileged -v /home/centos/blog:/home/blog ruby bash
```

### Explanation:
- `-it`: Runs an interactive terminal session.
- `--name ruby-gem`: Names the container `ruby-gem` for easy reference.
- `--privileged`: Grants elevated permissions to the container (may not always be necessary).
- `-v /home/centos/blog:/home/blog`: Mounts the local directory `/home/centos/blog` into `/home/blog` inside the container.
- `ruby bash`: Uses the official Ruby image and starts a Bash shell.

## Inside the Container

Once inside the container, navigate to the mounted directory:

```sh
cd /home/blog
```

**Note:** Any changes made in this directory will reflect on the host machine, making it easy to edit files locally while running Jekyll inside the container.

## Next Steps
1. Install Jekyll and Bundler inside the container:

   ```sh
   gem install jekyll bundler
   ```

2. Verify the installation:

   ```sh
   ruby -v
   gem -v
   jekyll -v
   bundler -v
   ```

## Conclusion
By using a Docker-based environment, Jekyll can be developed and tested without installing dependencies directly on the host machine. This approach ensures a clean and reproducible setup.

*Note: Post finalized using LLMs (chatgpt)*