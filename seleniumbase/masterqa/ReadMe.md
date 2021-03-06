![](http://cdn2.hubspot.net/hubfs/100006/images/masterqa_logo-5.png "MasterQA")
## Automation-Assisted Manual QA

### MasterQA combines [SeleniumBase](http://seleniumbase.github.io/SeleniumBase/) automation with manual verification to greatly improve the productivity and sanity of QA teams.

When you can't fully automate your testing, use MasterQA to speed up your manual testing. 

![](http://cdn2.hubspot.net/hubfs/100006/images/hybrid_screen.png "MasterQA Example")

(Above: Actual screens from [masterqa_test.py](https://github.com/seleniumbase/SeleniumBase/blob/master/examples/masterqa_test.py) running against [xkcd.com](http://xkcd.com/1522/))

### Install SeleniumBase and run the example test:
```bash
git clone https://github.com/seleniumbase/SeleniumBase.git

cd SeleniumBase

pip install -r requirements.txt

python setup.py install

cd examples

nosetests masterqa_test.py --with-selenium  # (This defaults to Firefox)
```

At the end of your test run, you'll receive a report with results, screenshots, and log files. (Add ``--browser=chrome`` to your run command in order to use Chrome instead of Firefox, which requires Chromedriver installed.)

### Follow the [example test](https://github.com/seleniumbase/SeleniumBase/blob/master/examples/masterqa_test.py) to write your own tests:

```python
from seleniumbase import MasterQA

class MasterQATests(MasterQA):

    def test_xkcd(self):
        self.open("http://xkcd.com/1512/")
        for i in xrange(4):
            self.click('a[rel="next"]')
        for i in xrange(3):
            self.click('a[rel="prev"]')
        self.verify()
        self.open("http://xkcd.com/1520/")
        for i in xrange(2):
            self.click('a[rel="next"]')
        self.verify("Can you find the moon?")
        self.click('a[rel="next"]')
        self.verify("Do the drones look safe?")
        self.click_link_text('Blag')
        self.update_text("input#s", "Robots!\n")
        self.verify("Does it say 'Hooray robots' on the page?")
        self.open("http://xkcd.com/213/")
        for i in xrange(5):
            self.click('a[rel="prev"]')
        self.verify("Does the page say 'Abnormal Expressions'?")
```

You'll notice that tests are written based on [SeleniumBase](http://seleniumbase.com), with the key difference of using a different import: ``from seleniumbase import MasterQA`` rather than ``from seleniumbase import BaseCase``. Now the test class will import ``MasterQA`` instead of ``BaseCase``.

To add a manual verification step, use ``self.verify()`` in the code after each part of the script that needs manual verification. If you want to include a custom question, add text inside that call (in quotes). Example:

```python
self.verify()

self.verify("Can you find the moon?")
```

MasterQA is powered by [SeleniumBase](http://seleniumbase.com), the most advanced open-source automation platform on the [Planet](https://en.wikipedia.org/wiki/Earth).
