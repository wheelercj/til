+++
title = "Anki's new scheduler: FSRS"
date = 2025-01-31T13:20:31-08:00
+++

[Anki](https://apps.ankiweb.net/) has a relatively new card review scheduling algorithm called [Free Spaced Repetition Scheduler (FSRS)](https://docs.ankiweb.net/deck-options.html#fsrs). I only just enabled it, but from how others have described it, it seems to be straight up better than Anki's previous scheduling algorithm for learning speed and retention.

FSRS is easy to enable for new and existing decks; it only takes a few minutes. [Here are the instructions](https://github.com/open-spaced-repetition/fsrs4anki/blob/main/docs/tutorial.md). Enabling FSRS doesn't change Anki's interface at all (except for the review intervals, of course). You don't need to change anything about how you use Anki, maybe except one tiny thing: the FAQ under the instructions mentions that it's good to click the "Optimize" button in the FSRS settings once per month.

> Q12: How often should I re-optimize parameters?
> 
> A12: Once per month should be more than enough. A more sophisticated rule is to optimize after every 2^n reviews: after 512, then after 1024, then after 2048, etc. But the "one month" rule is simpler.
> 
> — [fsrs4anki/docs/tutorial.md at main · open-spaced-repetition/fsrs4anki](https://github.com/open-spaced-repetition/fsrs4anki/blob/main/docs/tutorial.md#repos-sticky-header:~:text=Q12%3A%20How%20often,rule%20is%20simpler.)
