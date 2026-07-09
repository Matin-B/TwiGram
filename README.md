# TwiGram

![PyPI - Version](https://img.shields.io/pypi/v/TwiGram)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/TwiGram)
![License](https://img.shields.io/github/license/matin-b/TwiGram)

TwiGram is a lightweight, zero-authentication Python library for extracting and downloading Twitter/X content. It bypasses the need for official API keys by leveraging the Twitter Syndication API to retrieve high-quality media links, clean text, and metadata.

## Features

* **Multi-Format Extraction:** Natively parses standard text, single photos, multi-photo albums, GIFs, and HLS/mp4 videos.
* **URL Resolution:** Automatically resolves `t.co` short links and sanitizes `twitter.com` URLs to the `x.com` format.
* **Media Sorting:** Parses `.mp4` variants and sorts video output arrays by highest resolution automatically.
* **Network-Efficient Sizing:** Calculates human-readable file sizes via HTTP `HEAD` requests before initiating full payload downloads.

## Requirements

* Python 3.6+
* [requests](https://requests.readthedocs.io/en/latest/)

## Installation

```console
pip install TwiGram

```

## Usage

The library exposes a single primary function: `download()`.

### Basic Extraction

Pass a valid X (Twitter) status URL to retrieve the payload.

```python
from twigram import download

tweet_data = download("https://x.com/i/status/1481722124855169028")
print(tweet_data)

```

### Media Size Calculation

For applications requiring preemptive storage allocation or user prompts, set `show_size=True` to execute network-level size calculations.

```python
from twigram import download

tweet_data = download("https://x.com/i/status/1481722124855169028", show_size=True)

if tweet_data.get("status") and tweet_data.get("type_name") == "video":
    highest_quality = tweet_data["data"]["video_urls"][0]
    
    print(f"URL: {highest_quality['url']}")
    print(f"Resolution: {highest_quality['resolution']}")
    print(f"Size: {highest_quality['human_size']}")

```
#### Error Handling

Failures (e.g., deleted tweets, private accounts, invalid URLs) return a unified error dictionary:

```python
{
    "status": False,
    "status_code": 404,
    "message": "Tweet is not found. It may have been deleted or made private."
}

```

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)** - see the `LICENSE` file for details.