---
title: "Make custom Skribbl.io word banks using Reddit and Praw"
date: 2020-12-28
tags: ['blogs', 'Python']
draft: false
---

[Skribbl.io](https://skribbl.io/) is a great free quarantine / social distanced 
game where one person attempts to draw a word while everyone else guesses what they
are drawing. When setting up the game you can supply your own list of comma
separated words doing the game. 

The problem with doing this manually is that one person playing will know all
the words. 

For an upcoming Zoom party I created a python command line application that
takes in subreddit names and a few other parameters and using the
[Praw](https://praw.readthedocs.io/en/latest/) library retrieves the most
commonly used words from the top comments of posts to a subreddit.

Since subreddits are generally devoted to a specific topic you can easily
create pseudo-themed word banks by pulling comments from a category of
topics and selecting subreddits under that banner. 

You can download the program from the [GitHub page](https://github.com/EthanHolleman/Rskribbl).

## Usage

### Install dependencies

The only dependcy you need is `Praw`. Install it with the command below.

```
pip install praw
```

### Setup API keys

If you want to run the program yourself you will need to get a `client id` and
`client_secret` to use the Reddit API through Praw. The tutorial below has
all the info you need (you only need to watch the setup portion). 

{{< youtube NRgfgtzIhBQ >}}

To be able to post this project on GitHub (relatively) safely I used environmental
variables to store the values or my Reddit API credentials. You can do the same
or modify the code of `collect_reddit_instance` function (shown below) in `collect.py`
to use your credentials.

```python
def create_reddit_instance():
    '''Create a Reddit instance using Praw library.

    Returns:
        Reddit: Reddit instance via Praw. Credentials set using environmental
        variables.
    '''
    return praw.Reddit(client_id=os.environ['PRAW_CLIENT_ID'],
                       client_secret=os.environ['PRAW_SECRET'],
                       user_agent=os.environ['PRAW_USER_AGENT']
                       )
```
Set values for `PRAW_CLIENT_ID`, `PRAW_SECRET` and `PRAW_USER_AGENT` or
modify the code directly with your credentials. 


### Run the program

Once you have that set up you are ready to run the program by 
executing the `run.py` file. The help menu it will print is below.

```
python run.py --help
usage: run.py [-h] [-r SUBREDDITS [SUBREDDITS ...]] [-n NUMBER_WORDS] [-mc COMMENT_LIMIT] [-o OUTPUT_DIR] [-f] [-p POST_LIMIT] [-l MIN_WORD_LENGTH]

Harvest frequently words from subreddit comments using Praw

optional arguments:
  -h, --help            show this help message and exit
  -r SUBREDDITS [SUBREDDITS ...], --subreddits SUBREDDITS [SUBREDDITS ...]
                        List of subreddits to pull comments from
  -n NUMBER_WORDS, --number_words NUMBER_WORDS
                        Number of words to return per subreddit. Defaults to 25.
  -mc COMMENT_LIMIT, --comment_limit COMMENT_LIMIT
                        Max number of comments to harvest per subreddit. Defaults to 10,000
  -o OUTPUT_DIR, --output_dir OUTPUT_DIR
                        Output directory to write results to.
  -f, --include_occurrences
                        Include the number of times each word appears in the final output
  -p POST_LIMIT, --post_limit POST_LIMIT
                        Max number of posts to harvest from. Defaults to 50.
  -l MIN_WORD_LENGTH, --min_word_length MIN_WORD_LENGTH
                        Min word length. Defaults to 3 characters.
```

For example if I wanted to get the 10 most frequently used words from 100 comments 
from  `r/DataHoarder` I would use the command

```
python run.py -r "DataHoarder" -n 10 -mc 100
```

You can also specify multiple subreddits. The top word for each subreddit will
be written to a separate text files.

```
python run.py -r "DataHoarder" "Python" "arduino" -n 10 -mc 100
```

## Or use pre-harvested words

If you do not want to set up the program on your own computer I have already
created lists of 25 most used words with 5 or more characters 
from top comments of the 100 most popular subreddits.

You can download those files from the GitHib page here. Words are listed on a
single line separated by command for easier input into 

**NOTE**

*I have not reviewed all the words in these files and do not endorse
any of the content that may be found within, this is the internet after all.* 




