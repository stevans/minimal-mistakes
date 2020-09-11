---
layout: single
title:  "Quantifying the value of reinvesting paid dividends"
date:   2020-09-11
---
I’ve always been fascinated by finance and investing. This might have something to do with being raised by an accountant who would often preach the virtues of saving for retirement, but I’m not sure. My interest even led me to give a talk to my friends in the UT astronomy department titled [Do You Want to Buy A Yacht?: Saving for retirement 101](https://github.com/OttoStruve/gsps/blob/gh-pages/slides/stevans_retirement.pdf) for fun. 

Anyway, a few years ago I discovered “robo advisors” or computer applications that leverage automation and algorithms to manage your investments with increased efficiency. One feature that stood out to me was the ability to automatically reinvest earned dividends. Well, I was surprised to see that some roboadvisor brokerage sites like [M1 Finances](https://www.m1finance.com/) did not display the historical performance of stocks and funds assuming dividends were automatically reinvested.

This made me wonder, how would these historical performance plots look if dividend reinvestment was included? What is the potential value of reinvesting dividends with a stock or market fund with an average dividend? And, how would reinvesting dividends affect the returns of other popular investments like bonds or funds of high dividend stocks? I aimed to answer these question in this blog post.

To answer these questions I first had to gain access to stock data. After a bit of searching, I found a service called [Tiingo](https://www.tiingo.com/) that provides daily stock data via the python API [pandas-datareader](https://pandas-datareader.readthedocs.io/en/latest/index.html). <input type="checkbox" id="version" /><label for="version"><sup></sup></label><span>Version 0.7.0</span>

If you want to see the code I wrote to wrangle, analyze, and visualize the data, check out [**this Python Jupyter Notebook**](https://github.com/stevans/bernie-texas-2020/tree/master/notebooks) on my GitHub page. 
{: .notice--primary}


With Tiingo (and after signing up for an account and API token) I pulled the date, stock price, and dividend payment data.

Then I did the arithmetic to simulate dividend reinvestment. I designated the dividends to be reinvested at the opening price on the day after they were paid, so for each dividend payment I calculated the relative price increase (or decrease) at the end of each day after a dividend was paid. This array of price changes was then multiplied by the value of the dividend paid to get the daily value of the paid dividend. I then summed the daily value of the dividends to get the daily total value of all dividends.

With this script I can access the daily value of an investment in any stock or Exchange Traded Fund (ETF; an ETF is a collection of stocks similar to a mutual fund) assuming different treatment of the dividends: 1. exclude dividends, 2. add the value of dividends without reinvesting them, and 3. add the value of reinvested dividends. I can now remake the performance plots for any investment. The following figure shows what a $100 investment in Vanguard's all market ETF (ticker symbol: VTI) would be worth over time if invested on Jan 4, 2010 with the three previously mentioned treatments of dividends.

<iframe title="Reinvesting dividends increases returns significantly" aria-label="Interactive line chart" id="datawrapper-chart-htBjx" src="https://datawrapper.dwcdn.net/htBjx/3/" scrolling="no" frameborder="0" style="background: #FFFFFF; width: 0; min-width: 100% !important; border: none;" height="400"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"])for(var e in a.data["datawrapper-height"]){var t=document.getElementById("datawrapper-chart-"+e)||document.querySelector("iframe[src*='"+e+"']");t&&(t.style.height=a.data["datawrapper-height"][e]+"px")}}))}();
</script>


<!--- Added "background: #FFFFFF;" after style=" to secure a solid white background --->


This figure shows that automatic dividend reinvesting increases total returns or gains. In fact, for this particular ETF, the total gains from dividend reinvesting is 20% larger than the total gains when dividends were excluded and 7% larger than if dividends were included but not reinvested assuming no inflation. So, roboadvisors are leaving a significant value of their service, automatic dividends, out of their stock performance plots. <input type="checkbox" id="version" /><label for="version"><sup></sup></label><span>You might be thinking, but past dividends are not a guarantee of future dividends. And you would be correct, but it's also true that past capital gains of stocks are not a gaurantee of future capital returns. So, as long as historical performance plots are clearly labeled, I don't see an ethical problem with including dividends in historical performance plots. Better yet, these sites could add a toggle switch for the user to toggle between capital gains only and gains assuming reinvested dividends.</span>

What is the value of reinvesting dividends for other types of popular investments?

Although VTI is a good representative dividend investment because it is an all market ETF and therefore has a dividend that is equivalent to the volume-weighted average dividend, there are many ETFs with different goals, risks, and underlying assets or stocks. To see the impact of automatic dividend reinvesting on funds from a range of asset classes, I simulated the historical returns for a diverse set of ETFs from Vanguard, the Vanguard Select ETFs. I included two of Vanguard's dividend ETFs and a large-cap growth ETF for greater range of funds. 

For a simplified comparison, I calculated the average annual total return (AATR) over a 5 year period ending Aug 31, 2020. I used [the definition of AATR](https://personal.vanguard.com/us/glossary/a/GlossaryAverageAnnualTotalReturnContent.jsp) from Vanguard’s website. The following figure shows the 5-year AATR for the Vanguard ETFs broken down into three components: gains from capital only, gains from dividends only, and gains from reinvesting dividends. The ETFs are ordered by the AATR calculated excluding dividends.

<iframe title="Reinvesting dividends increases annual returns of ETFs by about 0.3%" aria-label="Split Bars" id="datawrapper-chart-QXEci" src="https://datawrapper.dwcdn.net/QXEci/1/" scrolling="no" frameborder="0" style=" background: #FFFFFF; width: 0; min-width: 100% !important; border: none;" height="806"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"])for(var e in a.data["datawrapper-height"]){var t=document.getElementById("datawrapper-chart-"+e)||document.querySelector("iframe[src*='"+e+"']");t&&(t.style.height=a.data["datawrapper-height"][e]+"px")}}))}();
</script>

<!--- Added "background: #FFFFFF;" after style=" to secure a solid white background --->

The right column of this figure shows that the ETFs' components of gains from reinvesting dividends range from 0.1% to 0.6%, with an average of 0.3%, and are small compared to their respective capital-only component and dividends-only component. <input type="checkbox" id="vug" /><label for="vug"><sup></sup></label><span>Expect for the Growth ETF (VUG) which has a relatively high reinvesting dividends component (0.6%) and a relatively small dividend-only component (0.8%).</span> This is consistent with the rationale that the gains from reinvesting dividends are fundamentally a multiplication of the capital-only gains and the dividends-only gains (i.e., two fraction multiplied together produce a smaller fraction). So, reinvesting dividends increases gains by a small amount for all asset classes, which can lead to significant gains when compounded over many years as illustrated in the first. Coincidentally, the average benefits of dividend reinvesting (0.3% a year) is about equal to the typical roboadvisor yearly fee (0.3%-0.6%), so we may have stumbled upon the reason M1 Finances doesn't display performance plots with the gains from reinvesting dividends. They don't want to sell you on a benefit that you won't actually received.

The figure also shows that the size of the reinvested-dividends component seems to be correlated more with the size of capital-only component than the size of dividend-only component. <input type="checkbox" id="cor" /><label for="cor"><sup></sup></label><span>In fact, the reinvested-dividends component is strongly correlated with the capital-only component (with an r correlation coefficient of 0.89) and is moderately anti-correlated with the dividends-only component (with an r correlation coefficient of -0.55).</span> At first, I was a little surprised by this since at face value I thought funds with larger dividends would be more impacted by dividend reinvesting. But now it make sense to me given that (again) gains from reinvesting dividends are fundamentally a multiplication of the capital-only gains and the dividends-only gains and that the ETFs with the largest capital-only gains (~12%) have decent dividends-only gains (~1.5%) while the ETFs with largest dividends-only gains (~2-3%) have relatively small capital-only gains (~2-5%) (i.e., `0.12*0.015=0.0018` is greater than `0.025*0.04=0.001`). This means that people invested in growth or all market funds have more to gain by reinvesting dividends than those invested in bond or dividend funds.

Here are the main take aways from this post:
1. Reinvesting the dividends of an all market ETF like VTI can grow your initial investment by 20% over ten years--7% more than if you kept your earned dividends in cash with no inflation.
2. People invested in a typical Vanguard ETF can grow their investment by an additional 0.3% annually by reinvesting their dividends.
3. If you use a roboadvisor, the average benefit of automatic dividend reinvesting will likely be cancelled out by the roboadvisor fee.
4. Reinvesting dividends is more profitable with more risky funds (i.e., growth or all market) over less risky funds (i.e., bonds or dividend stocks).






















