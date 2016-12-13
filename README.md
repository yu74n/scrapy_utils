# scrapy_utils

## Description
Utilities for scrapy

## Module
### Middleware
#### GithubOAuthMiddleware
Make OAuth authentication with Github API token

### Extension
#### GithubRateLimitWatcher
Watch GitHub Rate Limit in GitHub API header and close the connection for crawling if Rate Limit is over the limit user set in Scrapy setting file.

## Usage

### GithubOAuthMiddleware

#### Prerequisite
Get Github API OAuth token. Please refer to [Github Developer OAuth](https://developer.github.com/v3/oauth/) or [Github Developer Getting Started](https://developer.github.com/guides/getting-started/#authentication)

#### Setup
Create the `middlewares` directory under your spider folder.
```bash
mkdir -p <your_spider>/middlewares
```
Copy github_oauth.py under the `middlewares` directory.
```bash
git clone https://github.com/yu74n/scrapy_utils.git
cp scrapy/downloadermiddlewares/github_oauth.py <your_spider>/middlewares
```
Open your spider's setting.
```bash
vi <your_spider>/settings.py
```

Add Middleware name to `DOWNLOADER_MIDDLEWARES` in settings.py like
```
DOWNLOADER_MIDDLEWARES = {
    '<your_spider>.middlewares.github_oauth.GithubOAuthMiddleware': 290,
}
```

Set your Github API token to `oauth_token` variable in your spider code
```python
class YourSpider(scrapy.Spider):
    ...
    oauth_token = "xxxxxxxxxxxxxxxxxxxxxxxxx"
    ...
    def start_requests(self):
        ...
```

### GithubRateLimitWatcher

#### Setup
Create the `extensions` directory under your spider folder.
```bash
mkdir -p <your_spider>/extensions
```
Copy github_oauth.py under the `extensions` directory.
```bash
git clone https://github.com/yu74n/scrapy_utils.git
cp scrapy/extensions/github_rate_limit_watcher.py <your_spider>/extensions
```
Open your spider's setting.
```bash
vi <your_spider>/settings.py
```

Add Extension name to `EXTENSIONS` in settings.py like
```
EXTENSIONS = {
    '<your_spider>.extensions.github_rate_limit_watcher.GithubRateLimitWatcher': 500,
}
```

#### Setting
##### GITHUB_RATE_LIMIT_WATCHER_LIMITCOUNT
`X-RateLimit-Remaining`(please refer to [Rate Limit](https://developer.github.com/v3/#rate-limiting) describes the number of requests remaining you can send with GitHub API. 
When `X-RateLimit-Remaining` reaches `GITHUB_RATE_LIMIT_WATCHER_LIMITCOUNT`, your crawler will be closed.
