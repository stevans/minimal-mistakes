---
layout: single
title:  "Using US Census data to investigate the drop in youth-voter turnout in 2020"
date:   2020-4-1
---


After Super Tuesday, young voters were frequently scapegoated by media outlets for Bernie Sanders’s loses in Super Tuesday contests like in this US Today [article](https://www.usatoday.com/story/news/politics/elections/2020/03/04/super-tuesday-bernie-sanders-youth-votes-fell-short-compared-2016/4947795002/) entitled, *Many young voters sat out Super Tuesday, contributing to Bernie Sanders’ losses*. Their reasoning was that a lot of [polling](https://nymag.com/intelligencer/2020/02/this-one-chart-explains-why-young-voters-back-bernie-sanders.html) before Super Tuesday showed Sanders with a large support gap, being strongly favored by younger voters and strongly disfavored by older voters. So, for Bernie to have lost, young people must not have made it to the polls. At first glance, exit (and entrance) polling from CNN seems to support this notion. The percentage of voters aged 18 to 29 years old in states that voted on or before March 10th in both [2016](https://www.cnn.com/election/2016/primaries/polls/) and [2020](https://www.cnn.com/election/2020/entrance-and-exit-polls/) are displayed in the following table. We see that youth voters made up a smaller percentage of 2020 voters in 13 of the 15 states.

<iframe title="Youth voter turnout in Democratic Primaries has dropped in terms of percentages" aria-label="Table" id="datawrapper-chart-xoMeU" src="//datawrapper.dwcdn.net/xoMeU/2/" scrolling="no" frameborder="0" style="background: #FFFFFF; width: 0; min-width: 100% !important; border: none;" height="774"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"])for(var e in a.data["datawrapper-height"]){var t=document.getElementById("datawrapper-chart-"+e)||document.querySelector("iframe[src*='"+e+"']");t&&(t.style.height=a.data["datawrapper-height"][e]+"px")}})}();
</script>

<!--- Added "background: #FFFFFF;" after style=" to secure a solid white background --->

<!--- {% include figure image_path="/assets/images/posts/youth-vote/youth_voter_turnout_wtitle.png" alt="Three column table showing youth voter turnout in 2016 and 2020 and the difference." width="200" caption="Voter Turnout for 18-29 year-olds in Democratic Presidential Primaries. Sources: [[1]](https://www.cnn.com/election/2016/primaries/polls/) [[2]](https://www.cnn.com/election/2020/entrance-and-exit-polls/)" %} --->

<!--- <a href="{{ site.baseurl }}/assets/images/youth_vote_post/youth_voter_turnout_wtitle.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" width="200" src="{{ site.baseurl }}/assets/images/youth_vote_post/youth_voter_turnout_wtitle.png" caption="Voter Turnout for 18-29 year-olds in Democratic Presidential Primaries. Sources: [[1]](https://www.cnn.com/election/2016/primaries/polls/) [[2]](https://www.cnn.com/election/2020/entrance-and-exit-polls/)"/></a> --->

<!--- <figure class="figure">
  <img src="/assets/images/youth_vote_post/youth_voter_turnout_wtitle.png" style="margin-left: 5em; margin-right: 5em; max-width: 200px;"
       alt="Three column table showing youth voter turnout in 2016 and 2020 and the difference." align="middle"/>
    <figcaption>
      {{"Voter Turnout for 18-29 year-olds in Democratic Presidential Primaries. Sources: [[1]](https://www.cnn.com/election/2016/primaries/polls/) [[2]](https://www.cnn.com/election/2020/entrance-and-exit-polls/)" | markdownify }}
    </figcaption>
</figure> --->

<!--- While the margin of error of exit polls is typically 3-4%, averages are more robust. The average difference in youth voter turnout in these 15 states is -2.4%. Weighted by the number of 2020 voters in each state, the weighted average is even larger, -2.8%. --->

At the same time, when you consider the total number of young voters who cast votes in these 15 contests, you see that more young voters voted this year than 4 years ago. For example, in Texas the youth turn out went down 5% but the total number of youth voters increased by about 25,000. So how can both changes be true? Of course, it means that older voters had a larger increase in number (and percentage) than youth voters in 2020. This made me wonder, could this be explained simply by the fact that the US population is [aging](https://www.census.gov/newsroom/blogs/random-samplings/2016/06/americas-age-profile-told-through-population-pyramids.html), if all else is held equal to 2016? Or, has the propensity to vote of older voters change, too? And, how will projected demographic changes effect electorate compositions in future elections?

To begin to answer these questions, I turned to the Census Bureau, which has estimated the population of the US since it was founded in 1902 and published their population estimates [online](https://www.census.gov/). I was able to scrape together the US population broken down by single year of age since the year 1900. Given that the data was collected at various times over more than a century, the data isn’t perfectly homogenous in structure. For example, the only available data from 1900-1929 exclude Armed Forces overseas and the population residing in Alaska and Hawaii, the 1930-1959 numbers include Armed Forces overseas but exclude the population residing in Alaska and Hawaii, and the 2010s data has the most granular demographic breakdowns of the population of all decades (down to metropolitan division scales). I decided to use the data that include Armed Forces overseas in this analysis when available because, in principle, the Armed Forces could vote (although, in practice, I suspect it has been difficult to impossible). Methods for accessing the data vary, too; from excel spreadsheets on a webpage, like for [1900-1979](https://www.census.gov/data/tables/time-series/demo/popest/pre-1980-national.html), to an array of Census Population Estimates [APIs](https://www.census.gov/data/developers/data-sets/popest-popproj/popest.html) for years 1990 to 2019. 

**Check it out!** The python code I used to corral and clean the data can be found in a Python Jupyter Notebook on my GitHub page [here](https://github.com/stevans/youth-voters-census-data/blob/master/notebooks/Exploring_census_data.ipynb). 
{: .notice--primary}

With the US population per single year of age in every year from 1900 to 2020 (and projected out to 2060), I was able to calculate and plot the fraction of the population that falls in the category of youth voter (aged 18-29). 

{% include figure image_path="/assets/images/posts/youth-vote/youth_fraction.png" alt="Plot of the fraction of the US population aged 18-29 from 1900-2060." caption="Fraction of the US population aged 18-29 years old." %} 

To first order, the most obvious feature of this plot is the general trend downwards from 37% in 1900 to 21% in 2020. The next most significant feature is the large bump from about 1965 to 1995, when the Baby Boomer generation aged into and then out of the 18-29 age range. Also noticeable in the figure is a relatively small dip around 1918, when more than 4 million (mostly young) service people were overseas fighting in WWI. This is the only wartime period associated with such a dip in the figure because the census population worksheets I found include the population of Armed Forces overseas after 1940. 

Since 1972, when the major parties officially tied their convention delegates to the outcomes of state primaries, the fraction of the population comprised of 18-29 year-olds has decreased from 29% to 21%. This means that young people were outnumbered by all other voters ~2:1 in 1970 and are outnumbered by ~4:1 today.

## Can the aging US population explain the drop in youth voter turnout between 2016 and 2020 alone?

The short answer is, "No." I found the population aged 18-29 has shrunk by ~266,000 from March 3, 2016 to Mar 3, 2020 (by interpolating the yearly Census data) and the 30-and-over population has grown by ~8,774,000 in the same timespan. In terms of the youth voter fraction of the electorate, this results in a decrease of ~0.7% from 21.6% on Super Tuesday in 2016 (March 1) to 20.9% in on Super Tuesday in 2016 (March 3). Furthermore, if all voter demographic groups voted at the same rates as in 2016 (historical voting rate estimates from the Census Bureau were found [here](https://www.census.gov/data/tables/time-series/demo/voting-and-registration/voting-historical-time-series.html)), the youth turnout would appear to decrease by only ~0.5% in 2020 simply due to changes in the population age distribution. Since this is less than the 2.8% drop in the median youth voter turnout seen in 2020 exit polling compared to 2016, something in addition to age distribution change is needed to fully explain how the youth voter turnout could decrease in percentages while increase in total numbers. As mentioned earlier, the simple explanation is that older voters voted at a higher rate than they had four years ago. This seems very likely to me, as I suspect it is easy for the ~70% of the oldest population that votes to recruit a few percent of their cohort to join them at the polls than it is for the voting ~30-40% of 18-29-year-olds to get an equivalent number of their peers to vote.

## How will projected demographic changes effect electorate compositions in future elections?

Looking at the youth fraction plot at years after 2020, we see a steady decline to about 17% in 2060. That's 4.6% less than it is today. This suggests that all future presidential campaign relying on the youth vote will have an even taller task than Bernie had in 2020.