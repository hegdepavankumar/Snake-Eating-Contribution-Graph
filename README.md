# Snake-Eating-Contribution-Graph
How to enable GitHub Actions on your Profile README for a snake-eating contribution graph 🐍
#
github
#
markdown
#
opensource
#
tutorial
Git Good (9 Part Series)
1
Using the GitHub CLI to update your repo
2
How to create and pin a gist on GitHub
...
5 more parts...
8
How to use GitHub Pages to host your website, even with multiple repos
9
How to create a Profile README for your Organisation
Lots of people have been talking about and sharing their GitHub Profile READMEs. It was a project we launched last year and developers are loving it. As this feature became more popular, more developers were building templates, plugins, and apps for you to use on your profile.

This post from Supritha caught my attention. I like the way they talk about various pieces of code to have on your GitHub Profile README.

supritha 
How to have an awesome GitHub profile ?
Supritha Ravishankar ・ Jun 8 '21 ・ 5 min read
#github #markdown #opensource #git
One of the comments from Guillaume Falourd pointed to a really cool project from Platane.

GitHub logo Platane / snk
🟩⬜ Generates a snake game from a github user contributions graph and output a screen capture as animated svg or gif
snk
GitHub marketplace type definitions code style

Generates a snake game from a github user contributions graph



Pull a github user's contribution graph Make it a snake Game, generate a snake path where the cells get eaten in an orderly fashion.

Generate a gif or svg image.

Available as github action. Automatically generate a new image at the end of the day. Which makes for great github profile readme

Usage
github action

- uses: Platane/snk@master
  with:
    # github user name to read the contribution graph from (**required**)
    # using action context var `github.repository_owner` or specified user
    github_user_name: ${{ github.repository_owner }}

    # path of the generated gif file
    # If left empty, the gif file will not be generated
    gif_out_path: dist/github-snake.gif

    # path of the generated svg file
    # If left empty, the svg file will not be generated
    svg_out_path: dist/github-snake.svg
example with cron job

interactive demo


platane.github.io/snk

local

npm install
npm
…
View on GitHub
It uses GitHub Actions to build and update a user's contribution graph, and then has a snake eat all your contributions. The output generates a gif file, that you can then show on your GitHub Profile README. I thought this was pretty cool, so I set about adding this to my profile.

Step 1. Setting up GitHub Actions
The first thing you want to ensure before you start this project, is that you have GitHub Actions setup. Head to your Profile and ensure the "Actions" tab is available. Everyone should now have this feature.

Actions Button

Next, head to Platane's Action (available on the Marketplace) and make a copy of the code. You'll need to add this snippet into your Actions file.

Step 2. Creating your GitHub Actions yaml file
This is definitely the part where I got stuck. When looking at the code, I wasn't sure exactly where to add the lines of code mentioned on Marketplace.

After looking at the way Platane had their Actions file setup, I was able to generate the code (with a little help from Bdougie of course).

I've added the full code snippet below and added plenty of comments to (hopefully make it easy to understand).

You can copy this code straight into a blank *.yml file. Make sure you create a new *.yml file under the following directory:

YOUR_GITHUB_USERNAME --> .github --> workflows --> FILE_NAME.yml

# GitHub Action for generating a contribution graph with a snake eating your contributions.

name: Generate Snake

# Controls when the action will run. This action runs every 6 hours.

on:
  schedule:
      # every 6 hours
    - cron: "0 */6 * * *"

# This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:

    # Checks repo under $GITHUB_WORKSHOP, so your job can access it
      - uses: actions/checkout@v2

    # Generates the snake  
      - uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: Pavankumar-Hegde
          # these next 2 lines generate the files on a branch called "output". This keeps the main branch from cluttering up.
          gif_out_path: dist/github-contribution-grid-snake.gif
          svg_out_path: dist/github-contribution-grid-snake.svg

     # show the status of the build. Makes it easier for debugging (if there's any issues).
      - run: git status

      # Push the changes
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: master
          force: true

      - uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          # the output branch we mentioned above
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
Step 3. Running GitHub Actions
Once you've added the code above and committed it, head to your Actions tab. Under "Workflows", you should see the "Generate Snake" Action you created above.

Workflow

Click "Run Workflow" and watch your workflow run. You can even expand your workflow and see what's happening in real time.

GIFRunning Actions

Once your workflow has finished running, you should have received a green ✅ "build" checkmark. If so, this means your Action is working nicely. If not, you'll have to go through the code and see where the errors are. The "build" status should give you some indication of where your errors lie. You can also compare it with the yaml file on my GitHub Profile README.

Build green

If you have the green "build" ✅ then you should be good to go. Head back to your repo's "Code" directory, and change your branch to "output". Here you'll find the two versions of your contribution graph with the snake eating it: a *.gif and a *.svg. The good thing about these files is the file is rewritten over itself every time the Action runs. Thus, your contribution graph will always be up to date.

GIFCodeOutput

Step 4. Adding a contribution-eating snake to your profile
Now the final set is to add this to your profile. Grab the file location of your *.gif. It should be something like:

https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake.gif

Add this to your profile by copying the file location onto a new line in your markdown file:

![snake gif](https://github.com/Pavankumar-Hegde/Pavankumar-Hegde/blob/output/github-contribution-grid-snake.gif)

Now you should have a really cool looking snake eating your contributions!

GIFSnakeEating
Hopefully this guide was helpful for you and gives you a good base to start building and adding more Actions on your profile. What have you been adding to your GitHub Profile README? Other there other cool Actions I should be looking at?

Git Good (9 Part Series)
1
Using the GitHub CLI to update your repo
2
How to create and pin a gist on GitHub
...
5 more parts...
8
How to use GitHub Pages to host your website, even with multiple repos
9
How to create a Profile README for your Organisation



## Creators [🔝](#welcome-badges-4-readmemd-profile)

It's only possible because of [Shields Project](https://github.com/badges/shields), [Simple Icons](https://github.com/simple-icons/simple-icons) & beloved all [Contributors](https://github.com/Pavankumar-Hegde/Badges4-README.md-Profile/graphs/contributors). including [Authors](https://github.com/Pavankumar-Hegde) & [Collaborator](https://github.com/Pavankumar-Hegde). 

| [<img src="https://github.com/Pavankumar-Hegde.png?size=115" width="115"><br><sub>@Pavankumar-Hegde</sub>](https://github.com/Pavankumar-Hegde) |

