# Final Project Report
This is the culmination of all the work I've done this semester. Enjoy!

# Tables of Contents
1. [Project Summary](#summary)
    1. [Background](#back)
    2. [Hypothesis](#hyp)
2. [Process](#process)
3. [Analysis](#analysis)
    1. [Lexical Complexity](#lex)
    2. [Expressive Forms](#adj)
    3. [Hedges](#hedge)
    4. [Politeness](#polite)
    5. [Commands/Collaboration](#command)
4. [Abandoned Pursuits](#fails)
    1. [Exclamation, Question, Ellipsis Count](#punc)
    2. [Topic by Gender](#topics)
5. [Conclusion](#conclude)
6. [Further Analysis](#further)

## Project Summary <a name='summary'></a>
My project investigates gender differences in dialogue in Animated Movies. It looks at 12 Disney princess movies and 9 Dreamworks movies and whether female 
characters tend to adhere to what is thought of as traditionally "feminine" language.

### Background<a name='back'></a>
This project really started last semester. I was investigating how command use changed over time in Disney princess movies. I had to physically count all the 
commands uttered! It was exhausting... And since I was only looking at three movies, my findings weren't very significant. With bigger data, and the power of 
python, this project is meant to take my questions about gendered dialogue to the next level.

Specifically, I want to look at how female language use changes over time in these movies, how they vary based on production company, and if other factors like a 
character's role influence how they speak.
### Hypothesis<a name='hyp'></a>
Robin Lakoff created a list of features associated with female speech. (See my [powerpoint](link here) for a list used by Cameron and Kulick, 2003.) However, 
linguists have noted that these features are really features of powerless language (Eckert, Penelope, and Sally McConnell-Ginet. 2013. Language and Gender. 2Nd 
Edition. New York & Cambridge: Cambridge University Press).

I have three big questions:
* Do female characters use these "feminine" features more than male characters do depending on production company?
* Do Disney female characters use these features less often over time?
* Are some features attributable to whether a character is a protagonist or antagonist, and not male or female? 

My general hypothesis is: Both power and social circles play into these results. A female protagonist is more likely to be under the social microscope. She's 
someone you're supposed to look up to. As such, she will use the features typical of traditionally female speech. Female antagonists, on the other hand, exist 
outside of these social constraints. Unburdened from the social expectations of a "good" woman, and often in positions of power within their own social 
sphere, female antagonists will not exhibit these "feminine" features. Furthermore, as Disney has aged, social expectations of girls have changed. Their role 
models, the Disney Princesses, will reflect these changes in social expecatations. Similarly, many Dreamworks female protagonists are not princesses, nor are they 
the main character of the story. They also won't have to reach certain social expectations of the ideal girl. 

In summary: 
* Female Disney characters will use these feminine features less often in the later Eras of Disney.
* Female protagonists will use these features more often than female antagonists.
* Female characters in DreamWorks movies won't use these feminine features as often as Disney female characters.

## Process<a name='process'></a>

For the sources of my data, see [project_plan.md](https://github.com/Data-Science-for-Linguists-2019/Animated-Movie-Gendered-Dialogue/blob/master/project_plan.md).

This project involved a LOT of data cleaning. For how I annotated and edited by data, go to my code. The [Disney 
movies](https://github.com/Data-Science-for-Linguists-2019/Animated-Movie-Gendered-Dialogue/tree/master/code/Disney_code) was mostly annotation, with some web 
scraping for particularly messy data. The [DreamWorks 
movies](https://github.com/Data-Science-for-Linguists-2019/Animated-Movie-Gendered-Dialogue/tree/master/code/DreamWorks_code) were all scripts formatted as text 
files. I had to find a way to split these by line through [analyzing white 
space](https://github.com/Data-Science-for-Linguists-2019/Animated-Movie-Gendered-Dialogue/blob/master/code/DreamWorks_code/Analyzing_White_Space.ipynb).

Each entry in my dataframe contains the following: Text, the speaker, the gender of the speaker (male, female, or neutral), the role of the speaker 
(protagonist, antagonist, helper, or neutral), the status of the speaker (princess, prince, or neither), the year of the movie, the movie name, whether the line is 
song or dialogue, the line's utterance number in the film, and the movie's period. Period in this case only applies to Disney Movies. The 'EARLY' period in my data 
denotes Classic movies--Snow White, Cinderella, and Sleeping Beauty. The 'MID' period denotes Disney Renaissance movies--The Little Mermaid, Aladdin, Beauty and the 
Beast, and Mulan. The 'LATE' period denotes movies from the Disney Revival period--Princess and the Frog, Tangled, Frozen, and Moana.

In my final dataframe, I filtered out all songs and blank lines. Though songs are an important part of Disney movies, I decided to drop them for a couple reasons.
One, they are very repetitive, and this may influence some of my stats. Also, most Dreamworks movies don't have songs. I wanted to specifically look at
spoken dialogue between characters--I didn't need songs for this. 

My final dataframe is 13442 lines long, though not all lines were used in analysis. I wanted to look at gender and role, so when investigating these relationships, 
any characters not marked with a specific gender or role were dropped.

## Analysis<a name='analysis'></a>
For this analysis, I look at three different aspects of Lakoff's list, as well as lexical complexity and commands, which I investigated last semester. Specifically, 
I look at:
* Lexical Complexity: Token and Type Counts, TTR, and K-Band
* Expressive Forms: Adjectives
* Hedging
* Politeness: counts of polite phrases and apologies
* Collaboration and Indirectness: tag questions and different types of commands

### Lexical Complexity<a name='lex'></a>
My hypothesis:
* Disney female protagonists will have longer lines and better vocabulary than DreamWorks female characters. They are the main characters after all, right?
* Disney female protagonist token counts will go up over time, as they play a more active role in their movies.
* Female antagonists don't appear as much, and will have shorter lines.

First, let's look at a couple visualizations:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\overall_avg_tok_gen_role.png)
This suggests that female antagonists actually have longer lines than both male antagonists and female protagonists!

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\avg_ttr_role_gender.png)
Also, female antagonists seem to have higher TTRs than protagonists--male or female! Might this suggest a more refined vocabulary in villains?

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\avg_kband_gen_role.png)
K-Bands are also ways to measure vocabulary level, and here, the differences between males and females, and protagonists and antagonists, are very small.

Token Count by line seems to be significant! Of course, significance tests need to be performed to confirm or deny this. The following three tables are the results 
of [ttests](https://github.com/Data-Science-for-Linguists-2019/Animated-Movie-Gendered-Dialogue/blob/master/code/Significance_Tests_Token_Type_TTR.ipynb) on the 
features I used to track lexical complexity. Any significant tests are 
highlighted in green. Also note that the sign of the "stat" number is consistent with the order in which the comparison is listed. For instance, Disney M v DW M 
means a t-test was performed between male Disney characters and male Dreamworks characters. The first Stat value +3.19, implies that the average for male Disney 
characters 
was higher. The lower entry -2.67 indicates the average for Disney male characters was less than that of the male Dreamworks characters. 

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\lex_over_comp.png)

These results support my hypothesis concerning female Dreamworks and Disney 
characters.

From the Disney Female v DW Female column, we see that in Token Count by 
Line, Type Count by Line, Total Token Count, and Total Type Count, Disney 
female characters have consisently and significantly higher counts. 

Observe that by line, Disney male characters actually have a higher token 
count and a higher type count per line than female Disney characters! This 
seems to go against the idea that the main protagonist should have the 
longest lines. But also observe: when you look at total token and type 
counts per character, female Disney characters are significantly higher than 
male Disney characters. So, while male Disney characters may talk more 
inside each utterance, overall female Disney characters are talking the 
most.

Keeping this in mind, this would imply that female Disney characters speak 
longer per line than female Dreamworks characters, AND female Disney 
characters have more lines that female Dreamworks characters.

Notice, though, that female Disney characters don't have a higher TTR or 
K-Band than female Dreamworks characters. Overall, TTR and K-band were 
uninformative when it came to significant differences. The only exception 
here is looking at protagonists vs antagonists within each company. For both 
Disney and Dreamworks, protagonists have significantly lower TTRs than their 
antagonists. This may hint at a higher vocabulary for villains. Does this 
vary based on villain gender?

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\lex_overall.png)

It appears that female antagonists actually a significantly lower TTR 
than their male counterparts. And the ttest between female protagonists and 
antagonists show that there's no major differences in TTR. However, female 
antagonsits DO have a much higher token count per line than female 
protagonists.

The next question then would be: why is this? Do female antagonists hold the 
floor for longer because of the position of power? Perhaps they're less 
likely to be collaborative with others in the dialogue. Perhaps they're 
less likely to be interrupted. (For a failed look at interruption, see 
Abandoned Pursuits below). 

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\lex_over_era.png)

Though I thought that female token counts would go up over time, I've found 
that this isn't consistent over time. In looking at the last three columns 
comparing 
female characters over the early, mid, and late periods, we see that token 
and type count per line were actually significanlty higher in the early period 
than in the 
middle period, while the middle period's token and type counts per line were 
significantly less than those fo the late period. In contrast, we see that 
male token and type counts per line have gone up more 
consistently and significantly over 
time.

However, we do see that TTR for female characters is significantly higher in 
the late and mid periods than in the early periods. Though token count may 
not be consistent, the vocabulary used by the female characters has gone 
up. (Though this isn't unique to female characters--male TTR goes up over time as well).

Another interesting observation is that men have higher token and type counts per line than females in every era except the Earliest one! And in the early period, 
female characters had significantly higher total token and total type counts. A possible reason for this is the lack of male characters in the earliest era. Sure, 
there are princes, but they don't talk very much at all. That only leaves supporting male characters.

In fact, the distribution of characters by gender is an important thing to consider here. Consider the following graph of total line count by gender:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\total_lines_by_gen.png)

From the looks of this, male characters dominate! But when you normalize this over the number of characters of each gender, you get a very different picture:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\avg_num_line_by_gen.png)

We see that in several of the Disney movies, and even some Dreamworks movies, female characters individually average more lines than male characters. Considerations 
like this and token length stats were taken into account when doing the next portion of analysis: Adjective Counts.

### Expressive Forms<a name='adj'></a>
Do women really use more adjectives than men?
I hypothesize that 
* Female protagonists will use more adjectives than male protagonists
* Female Disney characters will use adjectives more than their DreamWorks counterparts
* Female Disney characters will use adjectives less often over time.
* Female villains will refrain from flowery language, and use fewer adjectives.

To assess my hypothesis, I decided I shouldn't use raw adjective counts per line. We saw in the bar graphs above that antagonists tend to have longer lines than 
protagonists, and 
male characters tend to have longer lines than female characters. The longer a line is, the more likely it is that more adjectives will appear in it. So, I decided 
I would divide the adjective count in each line by the token count of the line. Look at the differency this makes:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\adj_role_gen.png)

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\adj_over_tok_role_gen.png)

The differences between female and male antagonists, female and male protagonists, and female villains and heroes which seemed large in the first graph have been 
balanced out--and now aren't so significant. But they ensure that token count isn't influencing our results!

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\adj_over_all.png)
![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\adj_over_era.png)
![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\adj_over_comp.png)

These results actually contradict my hypothesis. From the Overall Adjective 
Use by Gender and Role Table, we see that male protagonists actually use 
more adjectives than female protagonists!

In terms of DreamWorks vs Disney, there's no significant differences in how 
females use adjectives. The only difference across companies is how 
protagonists use adjectives.

In terms of adjective use over time, we do see adjective counts for female 
Disney characters go down significantly between the early and late period. 
Though the drops in adjectives were not significant between the early and 
mid period or the mid period and the late period, these drops accumuluated 
over time to create a significant difference. Interestingly, in the late 
period, when female adjectives have dropped, men use significantly more 
adjectives than females. 

Also, it looks like female villains actually use more adjectives than female 
heroes (p = 0.0301). Perhaps villains like to be descriptive with their evil 
plots?

One concern I have with my adjective stat is how small it is. Raw adjective 
counts per line can already be low, but then dividing this further by token 
count makes the stat much smaller. As values shrunk, I thought that maybe I 
wouldn't get significant results, or perhaps skewed results. In the 
subsequent analyses, counts are also very small. 

### Hedges<a name='hedge'></a>
Unlike adjectives, I decided not to average hedge counts over token count, 
mostly 
because some hedges used were [not single words](link here to hedges 
notebook).

One aspect of this stats results that I have concern with is what it 
captures. In this analysis, I used a list of words and phrases. Some hedges 
can mean different things based on context. For instance, "well..." can be a 
hedge, but it isn't a hedge when a villain says "well, well, well..." Though 
I didn't account for this, it is something to take into account when looking 
at my results, perhaps with some skepticism.

Hedging is a method of saying something without taking a hard stand. I 
hypothesize that
* Disney female characters will use these more than Dreamworks female 
characters
* Female villains will use these less than female protagonists
* Female protagonists will use them more than men
* Female characters will use fewer hedges over time

A quick look at a bar graph comparing gender a role counts immediately puts 
my hypotheses about role into question:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\hedges_by_gen_role.png)

But this graph showing how hedge counts have changed over time shows that my 
hypothesis about female hedge count over time may be valid:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\hedge_over_era_gen.png)

It looks like females hedge less over time, while males hedge more over 
time. 

Let's look at hedges over time first:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\hedge_over_era.png)

Here, we see that female characters use hedges significantly less in the 
middle and late periods than in the early period. Though they also use fewer 
in the late period when comparing to the middle period, this difference is 
not significant. Also, we see on the far left of the graph that in the early 
period, men used significantly fewer hedges than women, but male use of 
hedges doesn't change significantly over time. This implies that hedge use 
between genders evened out in the middle and late periods not because both 
genders met in the middle, but because female characters stopped using them 
so much.

If we look at hedge use across companies, we see that there's no significant 
differences based on gender:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\hedge_over_comp.png)

In looking at gender and role overall, we see that differences occur when 
gender and role interact:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables\hedge_over_all.png)

Protagonists use more hedges than antagonists, but the difference between 
female protagonists and female antagonists isn't signficant. Oddly, female 
protagonists actually use hedges significantly less than male protagonists 
do, but female antagonists use significantly MORE hedges than male 
antagonists. This difference isn't simply attributable to gender or role. I 
personally have no idea why this might be, but it would be something 
interesting to investigate in the future.

### Politeness<a name='polite'></a>
These counts were also pretty low when I [found them](link here), so I 
didn't expect to get many significant results--but this ended up yielding 
some of the most significant results! I consider polite forms like "please" 
and "thank you" separately from apologies like "sorry". 

I hypothesized that:
* Female protagonists will apologize more and be more polite than male 
protagonists and female villains
* Disney females will be more polite than DreamWorks females
* Over time, female characters will apologize less and be less polite

From a quick look at the distributions, I'd say most of my hypotheses are on 
track:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\polite_by_gen_role.png)

Except for my politeness over time hypothesis. Female Disney characters seem 
to be getting more polite!

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\polite_by_gen_era.png)

Though, this may be influenced by token count. Like hedging, I did not 
average over token count.

Taking a look at the t-test results, we find some pretty significant 
differences:

![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables)
![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables)
![image](C:\Users\cassi\Desktop\Data_Science\Animated-Movie-Gendered-Dialogue\images\stat_tables)


### Commands/Collaboration<a name='command'></a>

## Abandoned Pursuist <a name='fails'></a>

## Conclusion <a name='conclude'></a>

## Further Analysis <a name='further'></a>
	