# Natural Language Toolkit (NLTK)
NLTK is a basic but useful python library for processing natural language texts. It can be installed using the command `pip install nltk`. This page lists some commands I often use in my NLP projects.

## Download related data
1. To download the "popular” subset of NLTK data, on the command line type

		python -m nltk.downloader popular
	or in the Python interpreter 

		import nltk; nltk.download('popular');
2. To download other datasets, run `nltk.download()` in the Python interpreter. Then a new download window should open. We can follow the displayed instructions and select some packages or collections to download.

## Tokenization
1. Word tokenizer

		>>> text = "Your name and e-mail address were configured automatically"
		>>> nltk.tokenize.word_tokenize(text)
		['Your', 'name', 'and', 'e-mail', 'address', 'were', 'configured', 'automatically']


2. Sentence tokenizer

		>>> text = "So amazing! It turns out to be a lot better than we expected."
		>>> nltk.tokenize.sent_tokenize(text)
		['So amazing!', 'It turns out to be a lot better than we expected.']


## Word count using FreqDist
1. Initialize the FreqDist object using a list of (tokenized) words.

		dist = nltk.FreqDist(['hello','world','!','this','is','a','sentence'])

	or using word tokenizer.

		dist = nltk.FreqDist(nltk.tokenize.word_tokenize(text))

	or if you want to uncase all the words,

		dist = nltk.FreqDist(w.lower() for w in nltk.tokenize.word_tokenize(text)) 

2. Find the frequency of a particular word

		>>> dist['hello']
		1

3. Find top-k most common words
		
		for (w, freq) in dist.most_common(k):
			print(w, freq)

	If we use only `dist.most_common()` without specifying `k`, it will list all the words and their counts (in the decreasing order).

4. Merge two FreqDist
		
		def merge_freqdist(fd1, fd2):
	    for (w, freq) in tqdm(fd2.most_common()):
	        fd1[w] = fd1.get(w, 0) + freq
	    return fd1

## WordNet
will be done.
## References

I would like to thank the authors of these helpful resorces which I used as references.

- [NLTK Book](https://www.nltk.org/book/)
- [NLTK Tokenization](https://www.guru99.com/tokenize-words-sentences-nltk.html) by guru99
- [NLTK WordNet](http://www.nltk.org/howto/wordnet.html)