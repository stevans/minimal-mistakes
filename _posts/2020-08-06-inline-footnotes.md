---
layout: single
title:  "Adding inline footnotes in HTML and CSS"
date:   2020-8-6
---

Click [here](#just-the-code) to jump to the section with the code.
{: .notice--success}

I really enjoy reading the blog [FiveThirtyEight](https://fivethirtyeight.com/) for the data-driven reporting on politics, sports, and life. It is also the first place I recall encountering the inline footnotes some time in 2017. I remember being way too impressed when I clicked on a footnote, the remaining article text lowered creating a blank space, and the footnote appeared out of thin air. Now that I have my own blog, I want to give my reads the same pleasurable experience. Since I don't know JavaScript, which 538 uses for their inline footnotes, my goal is to use HTML and CSS. In this post, I share what I've found for others who want to do something similar.

## FiveThirtyEight's Inline Footnotes
The FiveThirtyEight inline footnote feature allows a reader to view a footnote immediately after the footnote number by clicking on the footnote number. The reader can then hide the inline footnote by clicking on the "x" which appears in place of the clicked footnote number or continue scrolling through the text without hiding the footnote. Here is a GIF demonstarting how a reader can toggle a footnote in a 538 [article](https://fivethirtyeight.com/features/what-does-an-0-7-start-tell-you-about-an-nfl-coach/):

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/538-inline-footnote.gif){: .align-center}

 To me, this is an elegant way to include extra details for the interested reader without requiring the efficient reader to be distracted from the main idea of the article.

To replicate this on my own blog, I did what most people do--I Googled it. I found the basic HTML and CSS code I needed from the user Unrelated’s [answer](https://stackoverflow.com/questions/40336366/in-line-footnotes-with-only-html-css-in-notes/40391190#40391190) to the question "In-line footnotes with only HTML/CSS (in-notes?)” on Stack Overflow. To mimic the style of the feature on FiveThirtyEight I added some lines in the CSS to adjust the formating. Here is a GIF of how it looks on my blog:

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/my-blog-inline-footnote.gif){: .align-center}

Click on the following footnote to try it for yourself. <input type="checkbox" id="cb2" /><label for="cb2"><sup>2</sup></label><span><br><br>This is the footnote text.<br><br></span> This sentence (and the rest of the article) will move a few lines down. You can click the footnote number again to hide the footnote.



## The Code
Here is a template of the HTML code to insert within the text where you want the footnote number to appear:

```html
<input type="checkbox" id="cb1" /><label for="cb1"><sup>1</sup></label><span><br><br>This is the footnote text.<br><br></span>
```

And here is the CSS code with comments:

```markdown
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
