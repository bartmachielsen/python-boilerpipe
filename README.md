# python-boilerpipe


A python wrapper for [Boilerpipe](http://code.google.com/p/boilerpipe/), an excellent Java library for boilerplate removal and fulltext extraction from HTML pages.

## NOTE
**This fork contains a prepackaged boilerpipe version that is the latest version from the google repo. This fixes the problem with the getImages function.**

``jpype._jclass.java.lang.NoClassDefFoundError: java.lang.NoClassDefFoundError: de/l3s/boilerpipe/sax/ImageExtractor``

All credits for the actual code go to the original repo.

## Configuration


Dependencies:

 * jpype
 * chardet

The boilerpipe jar files will get fetched and included automatically when building the package.

## Installation

Checkout the code:

	git clone https://github.com/misja/python-boilerpipe.git
	cd python-boilerpipe


**virtualenv**

	virtualenv env
	source env/bin/activate
    pip install -r requirements.txt
	python setup.py install
	

**Fedora**

    sudo dnf install -y python2-jpype
    sudo python setup.py install


## Usage


Be sure to have set `JAVA_HOME` properly since `jpype` depends on this setting.

The constructor takes a keyword argment `extractor`, being one of the available boilerpipe extractor types:

 - DefaultExtractor
 - ArticleExtractor
 - ArticleSentencesExtractor
 - KeepEverythingExtractor
 - KeepEverythingWithMinKWordsExtractor
 - LargestContentExtractor
 - NumWordsRulesExtractor
 - CanolaExtractor

If no extractor is passed the DefaultExtractor will be used by default. Additional keyword arguments are either `html` for HTML text or `url`.

    from boilerpipe.extract import Extractor
    extractor = Extractor(extractor='ArticleExtractor', url=your_url)

Then, to extract relevant content:

    extracted_text = extractor.getText()

    extracted_html = extractor.getHTML()


For `KeepEverythingWithMinKWordsExtractor` we have to specify `kMin` parameter, which defaults to `1` for now:

	extractor = Extractor(extractor='KeepEverythingWithMinKWordsExtractor', url=your_url, kMin=20)


