---
layout: single
title:  "Adding inline footnotes in HTML and CSS"
date:   2020-8-6
---

Click [here](#just-the-code) to jump to the code.
{: .notice--success}

I really enjoy reading the blog FiveThirtyEight for their data-driven reporting on politics, sports, and life. A stylistic feature of their blog that I find makes for a more pleasurable experience is the inline footnote feature. I like it so much that I found a way to mimic the feature on my blog using HTML and CSS. Here I share what I found incase others want to do something similar.

## FiveThirtyEight's Inline Footnotes
The FiveThirtyEight inline footnote feature is basically where a footnote appears inline when the reader clicks on the footnote number. Here is a GIF demonstarting how a reader can toggle a footnote on the FiveThirtyEight site:

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/538-inline-footnote.gif){: .align-center}

 To me, this is an elegant way to include extra details that some may find interesting but that aren’t important to the main idea of the article. 

To replicate this on my own blog, I did what most people do--I Googled it. I found the basic HTML and CSS code I needed from the user Unrelated’s [answer](https://stackoverflow.com/questions/40336366/in-line-footnotes-with-only-html-css-in-notes/40391190#40391190) to the question "In-line footnotes with only HTML/CSS (in-notes?)” on Stack Overflow, and I added some lines in the CSS to mimic the style of the feature on FiveThirtyEight. Here is a GIF of how it looks on my blog:

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/posts/inline-footnotes/my-blog-inline-footnote.gif){: .align-center}

Click on the following footnote to try it for yourself. <input type="checkbox" id="cb1" /><label for="cb1"><sup>1</sup></label><span><br><br>This is the footnote text.<br><br></span> This sentence will move a few lines down.



## Just The Code
Here is a template of the HTML code:

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
