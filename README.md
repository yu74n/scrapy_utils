# scrapy_utils
Utilities for scrapy

## Module
### GithubOAuthMiddleware
Make OAuth authentication with Github API token

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

