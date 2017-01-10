# resurface.io on GitHub Pages
&copy; 2016-2017 Resurface Labs LLC

## Git Workflow

    git clone git@github.com:resurfaceio/resurfaceio.github.io.git ~/resurfaceio-website
    cd ~/resurfaceio-website
    git pull
    (make changes)
    ruby -run -e httpd . -p 9090              (ctrl-c to stop)
    git status                                (review changes)
    git add -A
    git commit -m "#123 Updated readme"       (123 is the GitHub issue number)
    git pull
    git push origin master                    (production site now updated)

When finished, use http://www.google.com/addurl to reindex each URL that was changed.

## Production Testing

Use Chrome developer tools to show all network requests (including redirects) for these tests.

These should load without a redirect:

    http://resurface.io
    http://resurface.io/index.html
    http://resurface.io/whale.jpg
    http://resurface.io/README.txt            (copyright statement only!)

These should load our custom 404 page without a redirect:

    http://resurface.io/bleep
    http://resurface.io/bleep/blorp

    http://resurface.io/.idea                 (existing private files)
    http://resurface.io/.idea/
    http://resurface.io/.idea/encodings.xml

These should load following a redirect:

    # default subdomain
    http://www.resurface.io                   --> http://resurface.io
    http://www.resurface.io/index.html        --> http://resurface.io/index.html
    http://www.resurface.io/whale.jpg         --> http://resurface.io/whale.jpg

    # default github pages subdomain
    http://resurfaceio.github.io              --> http://resurface.io
    http://resurfaceio.github.io/index.html   --> http://resurface.io/index.html
    http://resurfaceio.github.io/whale.jpg    --> http://resurface.io/whale.jpg

    # alternate domain 1
    http://resurfaceio.com                    --> http://resurface.io
    http://www.resurfaceio.com                --> http://resurface.io

    # alternate domain 2
    http://resurfaceio.org                    --> http://resurface.io
    http://www.resurfaceio.org                --> http://resurface.io

    # alternate domain 3
    http://resurfacelabs.com                  --> http://resurface.io
    http://www.resurfacelabs.com              --> http://resurface.io

    # alternate domain 4
    http://resurfacelabs.org                  --> http://resurface.io
    http://www.resurfacelabs.org              --> http://resurface.io

    # alternate domain 5
    http://usagelogger.com                    --> http://resurface.io
    http://www.usagelogger.com                --> http://resurface.io

    # alternate domain 6
    http://usageloggers.com                   --> http://resurface.io
    http://www.usageloggers.com               --> http://resurface.io

    # alternate domain 7
    http://usagelogging.com                   --> http://resurface.io
    http://www.usagelogging.com               --> http://resurface.io

These should load our custom 404 page following a redirect:

    # default subdomain
    http://www.resurface.io/bleep             --> http://resurface.io/bleep
    http://www.resurface.io/bleep/blorp       --> http://resurface.io/bleep/blorp

    # default github pages subdomain
    http://resurfaceio.github.io/bleep        --> http://resurface.io/bleep
    http://resurfaceio.github.io/bleep/blorp  --> http://resurface.io/bleep/blorp

    # alternate domain 1
    http://resurfaceio.com/bleep              --> http://resurface.io/bleep
    http://www.resurfaceio.com/bleep          --> http://resurface.io/bleep/blorp

    # alternate domain 2
    http://resurfaceio.org/bleep              --> http://resurface.io/bleep
    http://www.resurfaceio.org/bleep          --> http://resurface.io/bleep/blorp

    # alternate domain 3
    http://resurfacelabs.com/bleep            --> http://resurface.io/bleep
    http://www.resurfacelabs.com/bleep        --> http://resurface.io/bleep/blorp

    # alternate domain 4
    http://resurfacelabs.org/bleep            --> http://resurface.io/bleep
    http://www.resurfacelabs.org/bleep        --> http://resurface.io/bleep/blorp

    # alternate domain 5
    http://usagelogger.com/bleep              --> http://resurface.io/bleep
    http://www.usagelogger.com/bleep          --> http://resurface.io/bleep/blorp

    # alternate domain 6
    http://usageloggers.com/bleep             --> http://resurface.io/bleep
    http://www.usageloggers.com/bleep         --> http://resurface.io/bleep/blorp

    # alternate domain 7
    http://usagelogging.com/bleep             --> http://resurface.io/bleep
    http://www.usagelogging.com/bleep         --> http://resurface.io/bleep/blorp

## Image Production

### Generating Favicon Variations

http://realfavicongenerator.net solves what is otherwise a horrible chore.

    upload whalev_3color_320.png as the base image

    for iOS:
        use default settings

    for Android Chrome:
        select “Apply a slight drop shadow”
        app name = resurface.io
        theme color = #375a7f

    for Safari pinned tab:
        select “Turn your picture into a monochrome icon”
        turn threshold down to almost zero
        theme color = #375a7f

    for Windows 8 and 10:
        select “dark blue” color
        upload whalev_1color_inverted_320.png as dedicated image

Also use http://realfavicongenerator.net to check favicons after being integrated.

### Optimizing File Size

Run images through ImagOptim (includes zopfli) if you do nothing else.

Pixelmator can reduce image size further:

     apply “gaussian blur”
    apply "brightness" effect, contrast @ -10%
     apply "hue" effect, saturation @ -10%
     export to JPG @ 50% quality
    (then run through ImagOptim)

## Configuring Production From Scratch

### Create GitHub Repository

    Create resurfaceio GitHub user (if doesn't exist already)
        username = resurfaceio  (period not allowed here)
        email = resurfacelabs@gmail.com
        name = resurface.io
        url = http://resurface.io
        company = blank
        location = Boulder, CO

    As resurfaceio user, create new repository
        owner = resurfaceio
        repository name = resurfaceio
        description = Sources for http://resurface.io
        select "private" type of repository
        select "Initialize this repository with a README"

    As resurfaceio user, edit repository settings
        disable wikis
        add collaborators

    Log out of resurfaceio GitHub account (don't use this account for commits)

### Initialize GitHub Repository

    (clone repo first, see 'Git Workflow' section above)

    cd ~/resurfaceio-website
    echo "resurface.io" > CNAME
    echo "resurface.io" > index.html
    git add -A
    git commit -m "Add CNAME and index files"
    git pull
    git push origin master

    verify site now running at http://resurfaceio.github.io

### Configure DNS

    log into GoDaddy
    configure 'resurface.io' domain
    add A RECORD
        host = @
        points to = 192.30.252.153
    add CNAME RECORD
        host = www
        points to = @
    commit changes
    verify site now running at http://resurface.io

### Configure Alternate Domains

    log into GoDaddy
    for: { resurfaceio.com, resurfaceio.org, resurfacelabs.com, resurfacelabs.org,
           usagelogger.com, usageloggers.com, usagelogging.com }
        set domain and ‘www’ subdomain forwarding like this:
            forward to = http://resurface.io
            redirect type = 301
            forward settings = forward only
