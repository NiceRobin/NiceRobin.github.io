# Intro

I will be documenting my research on game development, written in English for practice. AI tools will aid me in correcting my syntax, with the original sentences listed beneath the improved sentences for comparison.

~~*i will do some record for my researching on game develop, it will write in english for practice
AI tools will help me to correct my sentences. the original sentences will also be listed under the correct one.*~~

# ML-Agents in Match-3 Games

Having perused the documentation and samples provided by ML-Agents, I noticed a match-3 game example and some basic structural code.

However, upon examining this code, I perceived that it only offers basic match rules, which may not necessarily be compatible with our game. Hence, I decided to start from scratch.

Having spent considerable time trying, I now think that might have been a misguided decision. I plan to revisit the sample code.

Since my knowledge of machine learning is rather limited, many of the parameters don't make much sense to me. My primary focus has been adjusting the sensors and actions, and waiting for results.

My first experiment was to train a model to identify opposing numbers. The results were mediocre but it helped me understand the basic operations of ML-Agents. I then shifted my focus to the match-3 game.

I tested different types of observations: vector and visual, as used in the sample. The results were disappointing, as the rewards plateaued after a certain threshold. Given the hours invested in each training session, I realized the need to test simpler cases.

Therefore, I began by identifying non-null elements on the board, a significantly simpler task. Here, I tasted success. The neural network consistently achieved winning results, and for the first time, I observed the correct pattern of the policy loss decreasing throughout the training.

However, the model seemed to only work on specific maps. On further investigation, I found that the neural network would identify one or two correct points and fixate on them. For instance, it would recognize that the point <5,5> was not null and halt there. My goal, however, was to identify all non-null points. Thus, while training was proceeding correctly, it was not producing the desired outcome.

This experience helped me understand the workings of neural networks. I also realized that static maps may not be the best approach, and I need to explore other methods.


~~*I have read ml-agents's documents and examples, it has a sample of match3 games, and provide some basic structural codes.
But when i looked at these codes, i thought it only provide a basic match rules, which may not fix our game. so i decided start from beginning.
After all these days trying, it may be a bad decision, so i will look at these codes again.
I did not know much details about machine learning, so the pramaters make no sence to me. The only thing that I can do is adjust sensors and actions, and wait.
Firstly I tried to train a model of finding opposite numbers. it works not very good, but it helped me to understood the basic operation of ml-agents. after that I move to match-3 game.
I trired different observations: vector and visual as the sample used. but the reuslt is not very good, the rewards stopped increase after reaching a line. every trainning use one or more hours, so I realized that I sould test some simpler case.
So I started finding not null elements in board, that task is much more simpler. and I successed. the neural network got a all win result. and for the first time I got the correct policy loss line which should getting lower while training.
But the model seemed only work on certain map, After some researching I found that the neural network will only find one or two correct point and stay there. For example, it will found that <5,5> was not null and stopped at there. but my goal was found all unnull points, So the training is right but wrong.
After that I realized the way of neural netwok. And the static map is not a good idea. I should find some other way.*~~