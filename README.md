# Discordoragi
Discordoragi is a Discord bot based on [Roboragi](http://github.com/Nihilate/Roboragi) which creates anime and manga links from MAL, Hummingbird, Anilist, MangaUpdates and Anime-Planet when requested.

## Installation
Discordoragi is written in Python for use with Python 3.5+ It is not possible to use anything less as the Discord API is phasing out support for it. There's a requirements.txt if you want to test it out yourself, but you'll need to create a Config.py with your own information and set up a PostgreSQL database.

###Step 1:
I recommend you install PyEnv if you are running linux, otherwise you can skip to step 3

```
[sudo] apt-get install git python-pip make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev
[sudo] pip install virtualenvwrapper

git clone https://github.com/yyuu/pyenv.git ~/.pyenv
git clone https://github.com/yyuu/pyenv-virtualenvwrapper.git ~/.pyenv/plugins/pyenv-virtualenvwrapper

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
echo 'pyenv virtualenvwrapper' >> ~/.bashrc
```
You will need to close out of the terminal (or start a new SSH session) to finish instalation
###Step 2:
Next we will install Python 3.5.1 using PyEnv

`pyenv install 3.5.1`

NOTE: This installs Python 3.5.1 in a virtual environment (venv) and it cannot be accessed from outside of the venv.

###Step 3:
Next we are going to install all of our dependencies

####Ubuntu
First we need to install some packages:  
`[sudo] apt-get install libffi-dev libxml2-dev libxslt-dev -y`

Now from the root directory of the repositoy run the following - Skip this if you are not using PyEnv:  
`pyvenv venv`  
`source venv/bin/activate`

We are now inside of our virtual environment with access to python 3.5.1.  
Type the following to install all of our dependencies:  
`pip install git+https://github.com/Rapptz/discord.py@async`  
`pip install -r requirements.txt`  

Test out our setup by running `python roboragi/AnimeBot.py`  
If you see `NameError: name 'MALAUTH' is not defined` then your setup is working up to this point!

####Windows
Run the following commands in a Command Prompt with Administrator Access  
`pip install git+https://github.com/Rapptz/discord.py@async`  
`pip install http://weebobot.no-ip.info/discordoragi/lxml-3.6.0-cp35-cp35m-win32.whl`  
`pip install http://weebobot.no-ip.info/discordoragi/pyquery-1.2.13-py2-none-any.whl`  
`pip install http://weebobot.no-ip.info/discordoragi/psycopg2-2.6.1-cp35-cp35m-win32.whl`  
`pip install -r requirements.txt`  

Test out our setup by running `python roboragi/AnimeBot.py` from the root directory of the repository.  
If you see `NameError: name 'MALAUTH' is not defined` then your setup is working up to this point!

###Step 4:
Setting up your config  
Copy the file `Config.py.example` to `Config.py`  
Open `Config.py` up and enter the information that it asks for, visiting the given websites when required  
You should be able to keep the `Database Info` the same if you are just testing, though you will want to change it if you are deploying.

###Step 5:
Creating your PostgreSQL Database

//TODO:

## How it works

Discordoragi uses discord.py (a Python library) to interface with Discord. It waits for messages from all of the servers it is allowed in and checks each of those for requests for the correct symbols - {}, {{}}, <> and <<>>. Once it's identified that it's being called, it takes the stuff between the braces and does a search for it in various anime/manga databases. Once it's got as much as it can find, the objects generated by the various databases are sent off to be formed into a reply. That then gets sent back to the channel it came from.

## Current databases
- MAL (Anime + Manga)
- Hummingbird (Anime)
- Anilist (Anime + Manga)
- MangaUpdates (Manga)
- Anime-Planet (Anime + Manga)