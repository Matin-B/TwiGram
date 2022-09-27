# TwiGram
Simple python package for download tweet from Twitter

## Install package
```console
pip install TwiGram
```

## Examples of How To Use 

Get tweet info

```python
from twigram import download

# Get tweet information from Twitter
download("https://twitter.com/i/status/1481722124855169028")
```


Get tweet info (show video size)

```python
from twigram import download

# Get tweet information from Twitter
download("https://twitter.com/i/status/1481722124855169028", show_size=True)
```