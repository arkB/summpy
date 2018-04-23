# Summpy

Text summarization (sentence extraction) module.
(Currently supports Japanese only)

## License

MIT License

Copyright (c) 2018 Recruit Technologies Co.,Ltd.

## Requirements 

### Python 3.6

+ numpy
+ scipy
+ scikit-learn
+ networkx
+ cherrypy
+ MeCab or janome
+ pulp (if you use ILP-based method)

### Input Parameters

- `text`: text (utf-8)
- `algo`: (optional)
  + `lexrank`: LexRank, a graph-based summarization (default)
  + `clexrank`: Continuous LexRank
  + `divrank`: (experimental) DivRank (Diverse Rank, graph-based method). Since DivRank aims to provide non-redundant and high coverage information, it is suitable for multi-document summarization.
  + `mcp`: ILP-based method. Extracts sentences in terms of Maximum Coverage Problem.

Hyper parameters for how many sentences are shown (optional) 

- `sent_limit`: number of sentences (only {lex,clex,div}rank)
- `char_limit`: number of characters
- `imp_require`: cumulative scores \[0.0-1.0\] (only {lex,clex,div}rank)

## Python API

### Example (Continuous LexRank)

```python
from summpy.lexrank import summarize

# ensure type(text) is unicode
sentences, debug_info = summarize(
    text, sent_limit=5, continuous=True, debug=True
)

for sent in sentences:
    print sent.strip().encode(encoding)
```

For further details, see `main` part of `summpy/lexrank.py` or `mcp_summ.py`.

## References

- G. Erkan and D. Radev. LexRank: graph-based lexical centrality as salience in text summarization. J. Artif. Int. Res. 22(1), pages 457-479, 2004. ([link](http://www.cs.cmu.edu/afs/cs/project/jair/pub/volume22/erkan04a-html/erkan04a.html))
- Q. Mei, J. Guo, and D. Radev. DivRank: the Interplay of Prestige and Diversity in Information Networks. In Proceedings of the 16th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining (KDD '10), pages 1009-1018, 2010. ([link](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.174.7982))

- H. Takamura and M. Okumura. Text Summarization Model Based on Maximum Coverage Problem and its Variant. In Proceedings of the 12th Conference of the European Chapter of the Association for Computational Linguistics (EACL '09), pages 781-789, 2009. ([link](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.222.6945))
