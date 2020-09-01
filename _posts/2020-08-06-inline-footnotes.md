---
layout: single
title:  "Adding inline footnotes with automatic numbering in HTML and CSS"
date: 2020-9-1 <!--- Orginally published on 2020-8-6 --->
---

**Updated!** Now includes automatic numbering.
{: .notice--success}

To jump to the section with the code, **click [here](#the-code)!**
{: .notice}

I really enjoy reading the blog [FiveThirtyEight](https://fivethirtyeight.com/) for the data-driven reporting on politics, sports, and life. It is also the first place I recall encountering inline footnotes some time back in 2017. I remember being way too impressed when I clicked on a footnote, the remaining article text lowered creating a blank space, and the footnote appeared out of thin air. Now that I have my own blog, I want to give my reads the same pleasurable experience. Since I don't know JavaScript, which FiveThirtyEight uses for their inline footnotes, my goal is to use HTML and CSS. In this post, I share what I've found for those who want to do something similar.

## FiveThirtyEight's Inline Footnotes
The FiveThirtyEight inline footnote feature allows a reader to view a footnote immediately after the footnote number by clicking on the footnote number. The reader can then hide the inline footnote by clicking on the "x" which appears in place of the clicked footnote number or continue scrolling through the text without hiding the footnote. Here is a GIF demonstarting how a reader can toggle a footnote in a FiveThirtyEight [article](https://fivethirtyeight.com/features/what-does-an-0-7-start-tell-you-about-an-nfl-coach/):

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/538-inline-footnote.gif){: .align-center}

 To me, this is an elegant way to include ancillary information or commentary for the interested reader without slowing down the efficient reader and distracting from the main idea of the article.

To replicate this on my own blog, I did what most people do--I Googled it. I found the basic HTML and CSS code I needed from the user Unrelated’s [answer](https://stackoverflow.com/questions/40336366/in-line-footnotes-with-only-html-css-in-notes/40391190#40391190) to the question "In-line footnotes with only HTML/CSS (in-notes?)” on Stack Overflow. To mimic the style of the feature on FiveThirtyEight, I added some lines in the CSS to adjust the aesthetics. Here is a GIF of how it looks on my blog:

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/my-blog-inline-footnote.gif){: .align-center}

Click on the following footnote to try it for yourself. <input type="checkbox" id="cb1" /><label for="cb1"><sup></sup></label><span><br><br>This is the footnote text.<br><br></span> This sentence (and the rest of the article) will move a few lines down. You can click the footnote number again to hide the footnote.



## The Code
Here is a template of the HTML code to insert within the text where you want the footnote number to appear:

```html
<input type="checkbox" id="cb1" /><label for="cb1"><sup></sup></label><span><br><br>This is the footnote text.<br><br></span>
```

Make sure the string after `id=` is unique AND matches the string after `for=`. Otherwise, clicking on any footnote link will do nothing or it will open (or close) the first occuring footnote at the position of the first occuring footnote. To get the padding or space infront of the footnote number, simply add a space before the input code.

And here is the CSS code with comments:

```markdown
/* This creates the counter  */
body {
  counter-reset: cb_counter_var;
}

/* This increments the counter value and defines 
the displayed content  */
sup::after {
  counter-increment: cb_counter_var;
  content: counter(cb_counter_var);
}

/* This initially hides the footnote (i.e. span)  */
input[type=checkbox] ~ span {
    display:none; 
}

/* This styles the footnote text which appears 
when the label is clicked  */
input[type=checkbox]:checked ~ span {
    display:inline; 
    font-size: 85%;
    font-family:$monospace;
    color: mix(#000, $text-color, 30%);
    cursor:default;
}

/* This permanently hides the checkbox  */
input[type=checkbox]{
    display:none;  
}

/* This styles the footnote label to appear 
like a hyperlink  */
input[type=checkbox] ~ label {
    display:inline;
    cursor:pointer;
    color:$link-color;
    text-decoration:underline;
}

/* This styles the footnote label when the mouse 
hover over it */
input[type=checkbox] ~ label:hover {
    text-decoration:underline;
    cursor:pointer;
    color:red;
}

/* This styles the footnote label after it is clicked */
input[type=checkbox]:checked ~ label {
    color:red;
    text-decoration:none;
}
```

If you’re using the Jekyll theme called Minimal Mistakes like I am, you can learn how to update the style sheet [here](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/) in the official Docs.

My next footnote-related adventure is to figure out how to get the footnote numbering sequence to update programmatically... **Update: I've implemented automatic numbering after discovering [CSS counters](https://www.w3schools.com/css/css_counters.asp).** Here is a second footnote number as a demostration of the autmoatic numbering. <input type="checkbox" id="cb2" /><label for="cb2"><sup></sup></label><span><br><br>Footnotes are cool.<br><br></span> 
