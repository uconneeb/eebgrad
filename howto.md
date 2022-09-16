---
title: How to make a GitHub Pages site
permalink: /eebgrad/howto/
layout: default
---
## How to set up a simple GitHub pages web site

These instructions show you how to create a simple GitHub Pages hosted web site. These instructions and the E.E.B. Grad web site were created to show new graduate students in the [Department of Ecology and Evolutionary Biology](https://www.eeb.uconn.edu) at the [University of Connecticut](https://www.uconn.edu) how to create a simple, easily-maintained, professional web site.

The web site itself can be viewed here: [https://uconneeb.github.io/eebgrad/](https://uconneeb.github.io/eebgrad/) and these instructions can be viewed by clicking on the link provided in the About page or by going to [https://github.com/uconneeb/eebgrad/](https://github.com/uconneeb/eebgrad/) and scrolling down to find a link to this same page.

Follow these steps to set up a basic Github Pages web site like the E.E.B. Grad site. If you encounter anything that doesn't work as described, please let me (Paul Lewis) know at [paul.lewis@uconn.edu](mailto:paul.lewis@uconn.edu).

## Download the files for this example

I will walk you through all the steps below, but you may wish to just clone the git repository for this example web site onto your local laptop just to get the big picture and see what your directory structure is supposed to look like when you are all done.

### Installing git if necessary

If you have a mac and typing <code>git</code> in a terminal window results in a message that says "command not found", then you will need to install git using, for example, [homebrew](https://brew.sh):

    brew install git

if you have Windows, your best bet is to install [Git for Windows](https://gitforwindows.org)

### Cloning the repository

If you have a functioning git program, navigate to the directory where you would like the code for this web site to reside and type the following in a terminal window:

    git clone https://github.com/uconneeb/eebgrad.git
    
This will create a directory named _eebgrad_ containing all the files. Once you create your site, cloning it like this should produce the same set of files with the exception of the file you are reading now, which I've left out of the instructions below because you do not need a copy of it on your web site.

## Sign up for an account at github.com

You'll need to supply a user name, an email address (to maintain portability, use your personal email address, not your UConn email address), and a password. Your ultimate web site will have the web address xxxx.github.io, where xxxx is your user name, so **choose the user name carefully**!


## Click the Create Account button

Leave everything set to the defaults (check unlimited public repositories for free, and don't check any checkboxes). Press the Continue button.

## Tailor your experience

Provide whatever information you want in this section, then press the Submit button.

## Click "Start a Project"

You'll be asked to confirm your email address before continuing further. This will involve clicking a link in an email that GitHub sends to the email address you supplied when you created your account.

## Choose a repository name

To create a web site, GitHub demands that you use a specific name for your repository: specify xxxx.github.io, where xxxx is **exactly** the same as the username you chose in step 1.

Keep "Public" checked (checking private will require you to pay money).

Be sure to check "Initialize this repository with a README".

You need not add a _.gitignore_ file at this time. It is easy to add one later if you need it.

Choose a license for your website. You can click the little "i" next to the drop-down list box to read about how to choose an open source license. If in doubt, you can avoid making a choice, but it is probably better to choose any of these options than to leave it set to None.

Press "Create Repository" to continue.

## Create an index page

The index page is the home page for your site. It is the page users see first when they type in the address of your site in their web browser. While logged into your site (https://github.com/xxxx), use the _Add file_ button to create a new file named _index.md_ and add the following text to it:

    {% raw %}---
    layout: home
    ---
    {% include figure.html description="<em>Pond at junction of Ravine and Bonemill west of the UConn Storrs campus in October, 2021.</em>" url="assets/images/cedar-swamp-pond.jpg" css="image-center noborder" width="800px" targeturl="https://eeb.uconn.edu/" %}
    
    [My CV](assets/PDFs/cv.pdf){% endraw %}
  
The file name extension _md_ stands for "markdown". You will write your web pages using a shorthand known as [markdown](https://en.wikipedia.org/wiki/Markdown) that will be translated by GitHub into the HTML that is served to your users. Writing in markdown relieves you of much tedium as it is almost like creating a document in a word processer application, but differs in that it is all plain text (you would not want to use Microsoft Word to edit your markdown file because it would be saved with a lot of (invisible) formatting commands and thus would not be a plain text file. When working with any of the files mentioned in this tutorial, you should either edit it using the editor provided by GitHub in your browser, or use a plain text editor such as [BBEdit](https://www.barebones.com/products/bbedit/) (mac) or [NotePad++](https://notepad-plus-plus.org) (windows).
  
The first three lines specify the "frontmatter". This is where you will specify such things as the titles for pages, permalinks, and layout information. The frontmatter for the _index.md_ page just specifies that this page should be laid out as the home page. Your GitHub Pages template will know what to do with that information.

The first line after the frontmatter in the _index.md_file is what is known as a liquid tag (starts with left-squiggly-bracket and percent symbol, and ends with the reverse). 

This liquid tag includes a file (_figure.html_) that is inside a directory named *_includes*. Note: neither the _figure.html_ file nor the directory *_includes* exists at this point, and so this line will not work just yet; we'll add the _figure.html_ file next.

The _figure.html_ file will contain HTML code for displaying an image and will provide a caption for the image as well as a web address (URL) that the user is taken to if the image is clicked. 

The _cv.pdf_ file also does not yet exist. We'll get to that soon too.

For now, be sure to save the contents you have added to the new file. You do this by typing a brief message (e.g. "added contents to the index page") in the first text box in the "Commit" section, then pressing the "Commit changes" button.

## Activate your web site

Click on the "Settings" link at the top and click on the "Pages" tab on the left. Choose the primer theme using the button provided. Don't agonize over the theme because we will switch to a different theme very soon.

## Allowing custom figure placement and annotation

### Creating the _figure.html_ file

The first line you added to the index page uses functionality in the file _figure.html_. Use the _Add file_ button and name the new file *_includes/figure.html*. This will not only create the file _figure.html_ but will also create the directory *_includes* in which the file will reside. Add the following text to the new file, then commit it:

    {% raw %}<div class="{{ include.css }}"><figure>
    {% if include.targeturl and include.height %}
        <a href="{{ include.targeturl }}"><img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" height="{{ include.height }}"></a>
    {% elsif include.targeturl and include.width %}
        <a href="{{ include.targeturl }}"><img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" width="{{ include.width }}"></a>
    {% elsif include.targeturl %}
        <a href="{{ include.targeturl }}"><img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" width="200px"></a>
    {% elsif include.height %}
        <img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" height="{{ include.height }}">
    {% elsif include.width %}
        <img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" width="{{ include.width }}">
    {% else %}
        <img class="{{ include.css }}" src="{{ site.baseurl }}{{ include.url }}" alt="{{ include.description }}" width="200px">
    {% endif %}
    <figcaption>{{ include.description }}</figcaption>
    </figure></div>{% endraw %}
    
This file is an HTML template. Note that the HTML code is riddled with commands that are bracketed by pairs of squiggly braces. For example, {% raw %}{{ include.targeturl }}{% endraw %} will be replaced by the <code>targeturl</code> specified in the liquid tag that included the _figure.html_ file, which, in the case of the one we employed in the _index.md_ file, is <code>https://goo.gl/maps/unTAUM14ueyUGbGN9</code>. 

### Creating the CSS needed to place the figure

You will notice that the liquid tag in _index.md_ that includes _figure.html_ specifies the Cascading Style Sheet (CSS) classes to be used: <code>css="image-center noborder"</code>. These serve to configure _figure.html_ to center the image on the page and to hide the border around the image. Right now, these CSS classes are not defined anywhere, so they will be ignored.  

Use the _Add file_ button to create a new file named *_sass/images.scss* and populate this file with the following CSS code, which will provide you with options for aligning the image to the left, center, or right side of the page, with or without a thin black border:

    div.image-left {
        text-align: center;
        display: inline-block;
        float: left;
        margin-right: 2rem;
        margin-bottom: 2rem;
        background-color: white;
    }

    img.image-left {
        border: 1px solid black;
    }

    img.image-left.noborder {
        border: 0;
    }

    div.image-center {
        text-align: center;
        margin-bottom: 2rem;
        background-color: white;
    }

    img.image-center {
        margin-left: auto;
        margin-right: auto;
        border: 1px solid black;
    }

    img.image-center.noborder {
        margin-left: auto;
        margin-right: auto;
        border: 0;
    }

    div.image-right {
        text-align: center;
        display: inline-block;
        float: right;
        margin-left: 2rem;
        margin-bottom: 2rem;
        background-color: white;
    }

    img.image-right {
        border: 1px solid black;
    }

    img.image-right.noborder {
        border: 0;
    }

Files (such as _images.scss_) saved in the *_sass* folder will not be used unless they are included from your _main.scss_ file. Use the _Add file_ button to create a new file named *assets/main.scss* and populate this file with the following:

    ---
    # Only the main Sass file needs front matter (the dashes are enough)
    ---
    @import "images";
    
As you can see, the only real line of any importance in this file is the line that imports the _images.scss_ file you stored in the *_sass* directory. The frontmatter (i.e. the two lines with dashes and whatever is between these two lines) is empty in this case (containing only a comment), but it nevertheless must be included.

## Adding your CV

GitHub does not let you create empty directories, so we'll sneakily create a dummy file in the directory we want to create and then later delete the dummy file once we've uploaded the CV file. Create a new dummy file named _assets/PDFs/dummy.txt_ in order to create the _PDFs_ directory. Upload a PDF version of your CV (named _cv.pdf_) into that directory. Once you have at least one other file in a directory, you can click on _dummy.txt_ and then click the trash can button to delete the _dummy.txt_ file. Be sure to always commit changes or else they will not take effect.

Once you've successfully uploaded your CV, edit _index.md_ and, if necessary, modify _assets/PDFs/cv.pdf_ to reflect the actual name of the PDF file you uploaded if you used a name other than _cv.pdf_.

## Adding an image

First, create or copy an image that you want to be the centerpiece of your home page and give it a name (the image I specified is _cedar-swamp-pond.jpg_, but your image file will probably have a different name; be sure that the name specified in the _index.md_ file matches the actual file name). I recommend resizing the image to at most 800 pixels wide using whatever software you use for playing with images (e.g. Photoshop, Preview, etc.). While it is not necessary to resize the image, smaller images will load faster for folks visiting your web site. 

Click on the _Add file_ button and then the _Create new file_ button and enter _assets/images/ dummy.txt_. Add some dummy text and commit the file. Now enter the _images_ directory and click the _Upload files_ button. Find your image file and upload it. You'll need to commit the change or else GitHub will ignore the upload. Once you've added the image to your _images_ directory, you can delete _dummy.txt_.

You've already added the appropriate line in your _index.md_ file to load this image, so in a minute or two your website should display your image.

## Adding a config file

There are a few more easy tweaks we can do by just creating a file named *_config.yml*. Create this file and populate it with the following text:

    theme: minima
    title: E. E. B. Grad
    email: eebgrad@uconn.edu
    description: Welcome to my professional web site!

    header_pages:
        - about.md
        - contact.md

    twitter_username: uconneeb

Note that we are switching the theme in the first line. The minima theme offers one feature not available in the primer theme, namely the ability to create a **main navigation menu**. To specify what links occur in that menu, create a list of markdown files named _header_pages_. Each of the files you list should exist and should have a title that is, idealy, just one word in length, as that title will be used as the text of the menu item that links to that page.

Specifying an email address and twitter username will result in these items being displayed in appropriate places in the footer of each page.

Let's go ahead and create the _about.md_ and _contact.md_ files.

Put some text in the _about.md_ file after you create it. Here is the text that is in the E.E.B. Grad web site's file, but you should probably change all of this except the first four lines:

    ---
    title: About
    layout: default
    ---

    I am a fictitious graduate student in the [UConn EEB department](https://eeb.uconn.edu) interested in the evolution, systematics, and ecology of seed and seedless plants, vertebrate and invertebrate animals, fungi, protists, and prokaryotes. I am also interested in developing ecological, phylogenetic, anatomical, and physiological methods.

    That photo of me below is a blend of 4 male and 4 female faces from diverse ethnicities using tools on the [faceresearch.org](https://faceresearch.org) web site.

    ![Image of E. E. B. Grad](/assets/images/headshot.png)
        
    [Back to Home](/)

Put something similar to the following text in the _contact.md_ file after you create it, being sure that the first four lines are not modifed:

    ---
    title: Contact
    layout: default
    ---

    Feel free to contact me at [eebgrad@uconn.edu](eebgrad@uconn.edu) but note that, because I am a fake person, and this is a fake email address, it is unlikely you will get a reply.

    Postal address: 

        E. E. B. Grad 
        Department of Ecology and Evolutionary Biology 
        University of Connecticut 
        Storrs, CT 06269-3043
        U.S.A.

    [Back to Home](/)

Be sure to commit these files.

## Some final tips

### Other resources

[Jekyll](https://jekyllrb.com) is the name of the web site generator system used by GitHub Pages to crunch your markdown file into the HTML files that are what is actually delivered to your users' browsers. GitHub Markdown is the particular "flavor" of markdown that is allowed on GitHub Pages sites.

* [Install Jekyll locally so that you can experiment](https://www.taniarascia.com/make-a-static-website-with-jekyll/)
* [GitHub Markdown Guide](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
* [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
* [Liquid Tags](https://shopify.dev/api/liquid/tags)

### Permalinks

It is easy to add a permalink to a page in the frontmatter. For example,

    {% raw %}---
    title: Contact Information
    permalink: /contact/
    layout: default
    ---{% endraw %}

If your website url is <code>https://xxxx.github.io/</code>, then the permalink we've specified means this page can be found using the url <code>https://xxxx.github.io/contact/</code>, regardless of the name of the file that this frontmatter is in.

### Comments

A pair of liquid tags that I've found very useful in markdown pages is the comment/endcomment combination:

    {% raw %}{% comment %}
    This text will not be shown.
    {% comment %}{% endraw %}
    
This allows you to comment out text that you want to have in the markdown but don't want rendered on the public-facing web site. Keep in mind that someone can still see this hidden text if they look at the markdown file in your Github repository, so don't use these tags to hide anything that you really don't want people to see.

### Code blocks

To create a code block in your markdown, just indent by four spaces:

    This is a code block
    
To show code in the middle of a sentence, you can wrap it in {% raw %}<code>HTML code tags</code>{% endraw %}. I'll use a code block to show you how to use the HTML code tags:

    ...you can wrap it in <code>HTML code tags</code>.

{% comment %}
## Adding a gem file

The final step is to create a file named _Gemfile_. Population _Gemfile_ with the following text and commit it:

    source "https://rubygems.org"

    gem "github-pages", group: :jekyll_plugins
    gem "webrick", "~> 1.7"
    gem "minima", "~> 2.0"
{% endcomment %}

