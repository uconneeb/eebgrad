## How to set up a simple GitHub pages web site

These instructions show you how to create a simple GitHub Pages hosted web site. These instructions and the E.E.B. Grad web site were created to show new graduate students in the [Department of Ecology and Evolutionary Biology](https://www.eeb.uconn.edu) at the [University of Connecticut](https://www.uconn.edu) how to create a simple, easily-maintained, professional web site.

The web site itself can be viewed here: [https://uconneeb.github.io/eebgrad/](https://uconneeb.github.io/eebgrad/) and these instructions can be viewed by going to [https://github.com/uconneeb/eebgrad/](https://github.com/uconneeb/eebgrad/) and scrolling down to see the rendered readme file contents.

## Steps

Follow these steps to set up a basic Github Pages web site like the E.E.B. Grad site. If you encounter anything that doesn't work as described, please let me (Paul Lewis) know at [paul.lewis@uconn.edu](mailto:paul.lewis@uconn.edu).

### Sign up for an account at github.com

You'll need to supply a user name, an email address (to maintain portability, use your personal email address, not your UConn email address), and a password. Your ultimate web site will have the web address xxxx.github.io, where xxxx is your user name, so **choose the user name carefully**!


### Click the Create Account button

Leave everything set to the defaults (check unlimited public repositories for free, and don't check any checkboxes). Press the Continue button.

### Tailor your experience

Provide whatever information you want in this section, then press the Submit button.

### Click "Start a Project"

You'll be asked to confirm your email address before continuing further. This will involve clicking a link in an email that GitHub sends to the email address you supplied when you created your account.

### Choose a repository name

To create a web site, GitHub demands that you use a specific name for your repository: specify xxxx.github.io, where xxxx is **exactly** the same as the username you chose in step 1.

Keep "Public" checked (checking private will require you to pay money).

Be sure to check "Initialize this repository with a README".

You need not add a .gitignore file at this time. It is easy to add one later if you need it.

Choose a license for your website. You can click the little "i" next to the drop-down list box to read about how to choose an open source license. If in doubt, you can avoid making a choice, but it is probably better to choose any of these options than to leave it set to None.

Press "Create Repository" to continue.

### Create an index page

The index page is the home page for your site. It is the page users see first when they type in the address of your site in their web browser. While logged into your site (https://github.com/xxxx), use the _Add file_ button to create a new file named _index.md_ and add the following text to it:

    {% include figure.html description="<em>A description of my photo.</em>" url="/images/homeimge.jpg" css="image-left noborder" width="800px" targeturl="https://eeb.uconn.edu/" %}

    [My CV](PDFs/cv.pdf)
    
The first line includes an image, providing a caption for the image as well as a web address (URL) that the user is taken to if the image is clicked. The _figure.html_ file that is referenced here does not yet exist, and so this line will not work just yet; we'll add the _figure.html_ file next.

The mycv.pdf file also does not yet exist. We'll get to that soon too.

For now, be sure to save the contents you have added to the new file. You do this by typing a brief message (e.g. "added contents to the index page") in the first text box in the "Commit" section, then pressing the "Commit changes" button.

## Activate your web site

Click on the "Settings" link at the top and click on the "Pages" tab on the left. Choose the primer theme using the button provided. Don't agonize over the theme because we will switch to a different theme very soon.

## Allowing custom figure placement and annotation

The first line you added to the index page uses functionality in the file _figure.html_. Use the _Add file_ button and name the new file *_includes/figure.html*. This will not only create the file _figure.html_ but will also create the directory *_includes* in which the file will reside. Add the following text to the new file, then commit it:

    <div class="{{ include.css }}"><figure>
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
    </figure></div>

## Adding your CV

GitHub does not let you create empty directories, so we'll sneakily create a dummy file in the directory we want to create and then later delete the dummy file once we've uploaded the CV file. Create a new dummy file named _PDFs/dummy.txt_ in order to create the _PDFs_ directory. Upload a PDF version of your CV (named _cv.pdf_) into that directory. Once you have at least one other file in a directory, you can click on _dummy.txt_ and then click the trash can button to delete the _dummy.txt_ file. Be sure to always commit changes or else they will not take effect.

Once you've successfully uploaded your CV, edit _index.md_ and, if necessary, modify _PDFs/cv.pdf_ to reflect the actual name of the PDF file you uploaded if you used a name other than _cv.pdf_.

## Adding an image

First, create or copy an image that you want to be the centerpiece of your home page and name it _homeimage.jpg_. I recommend resizing the image to at most 800 pixels wide using whatever software you use for playing with images (e.g. Photoshop, Preview, etc.). While it is not necessary to resize the image, smaller images will load faster for folks visiting your web site. 

Click on the _Add file_ button and then the _Create new file_ button and enter _images/ dummy.txt_. Add some dummy text and commit the file. Now enter the _images_ directory and click the _Upload files_ button. Find your _homeimage.jpg_ file and upload it. You'll need to commit the change or else GitHub will ignore the upload. Once you've added the image to your _images_ directory, you can delete _dummy.txt_.

You've already added the appropriate line in your _index.md_ file to load this image, so in a minute or two your website should display your image.

## Adding a config file

There are a few more easy tweaks we can do by just creating a file named *_config.yml*. Create this file and populated it with the following text:

    theme: minima
    title: E. E. B. Grad
    email: eebgrad@uconn.edu
    description: Welcome to my professional web site!

    header_pages:
        - about.md
        - contact.md

    twitter_username: uconneeb

Note that we are switching the theme in the first line. The minima theme offers one feature not available in the primer theme, namely the ability to create a main navigation menu. To specify what links occur in that menu, create a list of markdown files named _header_pages_. Each of the files you list should exist and should have a title that is, idealy, just one word in length, as that title will be used as the text of the menu item that links to that page.

Specifying an email address and twitter username will result in these items being displayed in appropriate places in the footer of each page.

Let's go ahead and create the _about.md_ and _contact.md_ files.

Put some text in the _about.md_ file after you create it. Here is the text that is in the E.E.B. Grad web site's file, but you should probably change all of this exept the first four lines:

    ---
    title: About
    layout: default
    ---

    I am a fictitious graduate student in the [UConn EEB department](https://eeb.uconn.edu) interested in the evolution, systematics, and ecology of seed and seedless plants, vertebrate and invertebrate animals, fungi, protists, and prokaryotes. I am also interested in developing ecological, phylogenetic, anatomical, and physiological methods.

    That photo of me below is a blend of 4 male and 4 female faces from diverse ethnicities using tools on the [faceresearch.org](https://faceresearch.org) web site.

    ![Image of E. E. B. Grad](images/headshot.png "Photo of E. E. B. Grad")

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

## Adding a gem file

The final step is to create a file named _Gemfile_. Population _Gemfile_ with the following text and commit it:

    source "https://rubygems.org"

    gem "github-pages", group: :jekyll_plugins
    gem "webrick", "~> 1.7"
    gem "minima", "~> 2.0"

