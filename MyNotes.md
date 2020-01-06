# Fake News Challenge: Stance Detection

- [challenge website](http://www.fakenewschallenge.org/)
- [dataset](https://github.com/FakeNewsChallenge/fnc-1)
- [baseline model github](https://github.com/FakeNewsChallenge/fnc-1-baseline)



## Goal

[notes from](https://github.com/srlakhe/Fake-News-Challenge) 

- use machine learning and/or deep learning for "stance" detection
    + Deep Learning - LSTM, Bidirectional LSTM? 
        - fully connected network with dropout
    + Gradient Boosting model for shared tasks (huh?)
        - [lightGBM](https://lightgbm.readthedocs.io/en/latest/)
        
- with a focus on feature engineering
- Word2Vec, Glove, fasttext (word embeddings? - pretty sure they are all the same so can just use word2Vec)
- TF-IDF
- custom features with polarity and n-gram counts ? 
- skip through sentence embeddings (to capture context)
- 

# FNC Winners
##### plenty to read here to learn
[Talso](https://github.com/Cisco-Talos/fnc-1)
[Athene System](https://github.com/hanselowski/athene_system)
[UCL](https://github.com/uclnlp/fakenewschallenge)



*******************************************************************************************************************************************

# Steps

    1. tokenize
    2. clean



# my preprocessing


## tokenize options

    

    1. nltk `word_tokenize` 
       * tokens = word_tokenize(text)
       * ds-02-22-11
       
    2. `nltk.regexp_tokenize`
       * e.g., pattern = "([a-zA-Z]+(?:'[a-z]+)?)"
       * macbeth_tokens_raw = nltk.regexp_tokenize(macbeth_text, pattern)
       * ds-04-37-06

## removing punctuation

- [using pythons builtin str.maketrans()](https://docs.python.org/3/library/stdtypes.html)
- ds 02-22-11 does it manually 

































# Useful Code Examples from prior lessons

from ds-02-22-11
This is removing lines that have the authors name in brackets [], puncutation marks and the new line characters \n

    def clean_song(song):
        cleaned_song = []
        for line in song:
            if not '[' in line and  not ']' in line:
                for symbol in ",.?!''\n":
                    line = line.replace(symbol, '').lower()
                cleaned_song.append(line)

        return cleaned_song

    song_without_brackets = clean_song(test_song)  #test_song is not in the repo!!!
    song_without_brackets
    
tokenize
    
    def tokenize(song):
    joined_song = ' '.join(song) # join is a builtin
    tokenized_song = word_tokenize(joined_song) #word_tokenize is an nltk method. Uses a Tree bank and Punkt
    
    return tokenized_song

tokenized_test_song = tokenize(song_without_brackets)


create a vector of bag of words (a dict. that keeps word order)

    def count_vectorize(song, vocab=None):
    if vocab:
        unique_words = vocab
    else:
        unique_words = list(set(song))
    
    song_dict = {i:0 for i in unique_words}
    
    for word in song:
        song_dict[word] += 1
    
    return song_dict

test_vectorized = count_vectorize(tokenized_test_song)





