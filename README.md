# Covid-19-Language-Model

This small project seeks to prepare a language model using the relevant research papers and articles currently available pertaining to the ongoing global Covid-19 pandemic. A multitude of datasets is used for this language model, the main source being the [COVID-19 Open Research Dataset Challenge (CORD-19)](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge). It contains a collation of all the relevant and useful research papers on the topic. Further, I have also taken references from some Kaggle notebooks: [Xhlulu's notebook](https://www.kaggle.com/xhlulu/cord-19-eda-parse-json-and-generate-clean-csv) provides the appropriate cleaned data that I required for the work and [Daniel Wolffram's notebook](https://www.kaggle.com/danielwolffram/topic-modeling-finding-related-articles) talks about topic modelling and finding related articles and papers.

## Workflow:

First the languages in which all the papers are written is detected. This is done by using the `detect` function of the [langdetect](https://pypi.org/project/langdetect/) library. It is found that all but four papers are written in English and the rest are written in Spanish. Since I am not proficient in Spanish and translating only four papers is largely an easy task, I translated them using the [Googletrans](https://pypi.org/project/googletrans/) library.

The language model comes prepared with basic understanding of English thanks to the [Fastai](https://www.fast.ai) library. The paper [Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146) argues that just like many applications in computer vision, language processing tasks can also be benefitted using transfer learning. So, the model is trained with Wikipedia text. In order to make it specific to my task, I train it on the Covid-19 papers data so that it identifies the nuances in these kinds of texts further. An [AWD-LSTM](https://arxiv.org/pdf/1708.02182.pdf) is used for this task particularly because it employs [DropConnect](http://yann.lecun.com/exdb/publis/pdf/wan-icml-13.pdf) and a variant of Average-SGD (NT-ASGD) along with several other well-known regularisation strategies.

Training is done using a 50% dropout rate for a total of 14 epochs using the cosine cyclical annealing method of fitting proposed in [Cyclical Learning Rates for Training Neural Networks](https://arxiv.org/abs/1506.01186) by Leslie Smith. Briefly explaining, cyclical annealing helps the model to examine the entire domain of a loss funtion to precisely know where to optimise. After 14 epochs, the model accuracy comes out to around 48%. For a language model, this accuracy is quite good because it tells that the model is predicting the correct next word almost half the time (which is great for textual data).

![Example](https://github.com/piyushmishra12/Covid-19-Language-Model/blob/master/example.png)

## Future Scope

The language model can further be used for carrying out document clustering and classification to help the frontline workers quickly find the appropriate research for the specific problem at hand.
