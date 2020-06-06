# Setting Up Your Development Environment

This week I got to install a fresh version of Ubuntu on my new machine. I want to record how I go about setting up my development environment here to save me the hassle of scratching my head and Googling around later. Here is, in a somewhat particular order, my dev essentials.

## Terminal

Setting up a terminal that is pleasing to look at is one of my creature comforts as a dev. Here is what I add to the `~/.bashrc` file.

```sh
alias "ls=ls --color=auto"
export PS1="\[\033[32m\]\u\[\033[m\]@\[\033[38m\]\h:\[\033[38;1m\]\w\[\033[m\] \$ "
export CLICOLOR=1
export LS_COLORS='di=32:ln=35:so=32:pi=33:ex=31:bd=34'  
```

## Git

After install run

```sh
$ git config --global user.name "James Wood"
$ git config --global user.email "email@example.com"
```

## Python

Setting up Python is a bit more involved. My goals with Python are to:
- Be able to switch between version with ease
- Be able to manage dependencies
- Be able to use Jupyter Notebooks 

In order to switch between versions with ease, I've found the best way to do this is pyenv.

Instructions:
https://realpython.com/intro-to-pyenv/
https://github.com/pyenv/pyenv

Note: I opted to check the repo out of GitHub.

```sh
$ pyenv global 2.7.X 3.8.X
```

To manage dependencies, I'm using venv. This locks in python version and packages which simplifies things greatly.

#### Example: Setting up my Jupyter Notebook venv
``` sh
python3 -m venv jupyter
source jupyter/bin/activate
pip install notebook 
```

Honestly, this was much easier than I remember it being.

## Ruby

## Dev Tools

The following aid me in my development work on a daily basis:
- Vim
- Postman
- VSCode
