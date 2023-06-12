# Wordle best word!.
what's the best word to start wordle with? is it "Furry"? or "House"? or Maybe "Clown"?
Today we're using **python** to find out.

## What's wordle? 
Wordle is a word-guessing game that has gained popularity in recent years. In the game, a player is presented with a blank grid of five rows and five columns, and a hidden five-letter word. The player has six chances to guess the word by entering five-letter words that they think might match the hidden word. After each guess, the game shows which letters in the guess match the hidden word and in what position. The objective is to guess the hidden word in as few attempts as possible.

You can try wordke using this link: https://www.nytimes.com/games/wordle/index.html

So, what's the best word to start this game with? let's find out!

# Step 1: Get all the possible words
the files 'words_alpha.txt' containes all the words in the english language, it containes exactly 370103 words. most of these words aren't useful for us, we need 5-letter words only, we extract them accordingly.

```py
words5 = []
for word in lines:
    word = word.replace("\n", "")
    w = word.replace("\n", "")
    if len(w) == 5:
        words5.append(w)
len(words5)
```
Good, we're left with 15918 words.
But wait! our word must not contain any repeated letters, remember, we want to get as much letters as we can in one word in order to increase our chances. So we remove any word that containes any repeated letters.

```py

wordsWithoutRepeated = []
for word in words5:
    w = ""
    for letter in word:
        if w.find(letter) == -1:
            w += letter
    if len(w) == 5:
        wordsWithoutRepeated.append(w)
len(wordsWithoutRepeated)
```


We're now left with 10173 words only, isn't that great? 

# Step 2: Calculate the weight of each letter in the alphabets.
The weight of each letter is the number of times it appears in the set of 10,137 words we have. This highlights the importance of each letter in the 5-letter words.

```py
weights = {}
for i in range(26):
    weights[chr(i+97)] = 0

for word in wordsWithoutRepeated:
    for letter in word:
        if (ord(letter) - 97) > -1:
            weights[letter] +=1
plt.bar (weights.keys(), weights.values())
```

And we get the following result
![twitter_c1117c3b0591a6b2b879f1088251d0fe](https://github.com/nehadyounis/wordle_best_words/assets/67816665/49f1d1b1-9995-4936-8436-82b704ff4bb3)

As you can see, The letter **A** is the most repeated letter in the set of 5-letter words. followed by the **E, S, R and I**

# Step 3: Getting the best word!
We are getting closer! To get the word, we now start by calculate the score of each word in the set. The scor of each word is the sum of weights of all the letters which the word is made of.
After calculating the weight of all words, we get the word with the max score.
```py
scores = {}
for word in wordsWithoutRepeated:
    for letter in word:
        scores[word] = scores.get(word,0) + weights.get(letter,0)
max_key = max(scores, key=scores.get)
max_key
```
Ready for the result?
🥁
🥁
🥁
## The word is: ✨**Arise**✨
Well, the word is actually aesir in this example, but I prefer to use arise as it's easier to remember and has got the same score. Also by setting the letters' weights in the word **arise** to 0, and recalculating the score, we get the second best word to use after we use arise, and the third .. etc.

Accordingly the best four words to use sequentally are: ✨**Arise**✨**Clout**✨**Nymph**✨**Badge**✨

And as you can see, this list is pretty useful when it comes to solving wordle.
![twitter_FKwd1F-WUAoB27N](https://github.com/nehadyounis/wordle_best_words/assets/67816665/7b7cf2fb-1b81-49cc-a1aa-58a6d1358f64)

## Thanks, and have an awesome day!


