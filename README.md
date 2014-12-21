pyspider [![Build Status][Build Status]][Travis CI] [![Coverage Status][Coverage Status]][Coverage] [![Try It Now!][Try]][Demo]
========

A Powerful Spider(Web Crawler) System in Python. **[TRY IT NOW!][Demo]**

- Write script in python with powerful API
- Python 2&3
- Powerful WebUI with script editor, task monitor, project manager and result viewer
- Javascript pages supported!
- MySQL, MongoDB, SQLite as database backend 
- Task priority, retry, periodical, recrawl by age and more
- Distributed architecture


Sample Code 
-----------

```python
from libs.base_handler import *

class Handler(BaseHandler):
    '''
    this is a sample handler
    '''
    @every(minutes=24*60, seconds=0)
    def on_start(self):
        self.crawl('http://scrapy.org/', callback=self.index_page)

    @config(age=10*24*60*60)
    def index_page(self, response):
        for each in response.doc('a[href^="http://"]').items():
            self.crawl(each.attr.href, callback=self.detail_page)

    def detail_page(self, response):
        return {
                "url": response.url,
                "title": response.doc('title').text(),
                }
```

[![Demo][Demo Img]][Demo]


Installation
------------

* python 2.6, 2.7, 3.3, 3.4
* `pip install --allow-all-external -r requirements.txt`
* `./run.py` , visit [http://localhost:5000/](http://localhost:5000/)

if you are using ubuntu, try:
```
apt-get install python python-dev python-distribute python-pip libcurl4-openssl-dev libxml2-dev libxslt1-dev python-lxml
```
ro install binary packages first.

[Full Deployment](http://pyspider.readthedocs.org/en/latest/Deployment/)

Documents
---------

* [Quickstart](http://pyspider.readthedocs.org/en/latest/Quickstart/)
* [API Reference](http://pyspider.readthedocs.org/en/latest/apis/)
* [docs](http://pyspider.readthedocs.org/)


TODO
----

### v0.3.0 (current)

- [x] as a package
- [x] run.py parameters
- [x] sortable projects list #12
- [x] Postgresql Supported via SQLAlchemy (with the power of SQLAlchemy, pyspider also support Oracle, SQL Server, etc)
- [x] benchmarking
- [x] python3 support
- [ ] documents
- [ ] pypi release version

### v0.4.0

- [ ] a visual scraping interface like [portia](https://github.com/scrapinghub/portia)


### more

- [ ] local mode, loading scripts from file.
- [ ] edit script with local vim via [WebDAV](http://en.wikipedia.org/wiki/WebDAV)
- [ ] in-browser debugger like [Werkzeug](http://werkzeug.pocoo.org/)

### ???
- [ ] works as a framework (all components running in one process, no threads)
- [ ] shell mode like `scrapy shell` 


Contribute
----------

* Use It
* Open [Issue], send PR
* [User Group]


License
-------
Licensed under the Apache License, Version 2.0


[Build Status]:         https://img.shields.io/travis/binux/pyspider/master.svg?style=flat
[Travis CI]:            https://travis-ci.org/binux/pyspider
[Coverage Status]:      https://img.shields.io/coveralls/binux/pyspider.svg?branch=master&style=flat
[Coverage]:             https://coveralls.io/r/binux/pyspider
[Try]:                  https://img.shields.io/badge/try-pyspider-blue.svg?style=flat
[Demo]:                 http://demo.pyspider.org/
[Demo Img]:             https://github.com/binux/pyspider/blob/master/docs/imgs/demo.png
[Issue]:                https://github.com/binux/pyspider/issues
[User Group]:           https://groups.google.com/group/pyspider-users
