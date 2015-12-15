Copyright &copy; 2016 Resurface.io LLC

ALL RIGHTS RESERVED

resurface.io README
===================

## <a name="techused"></a>Technologies Used

* What's used in development
    * Mac for official coding and local build/test
    * GitHub for source control & issue/release tracking
    * RubyMine for Ruby IDE
    * Pixelmator for image editing
    * Beyond Compare for diffing
* What's currently running in production
    * GitHub Pages for web server
    * Bootstrap/Bootswatch for responsive web UI
    * GoDaddy for domains, DNS, SSL
    * Loader.io for load testing

## <a name="gitworkflow"></a>Git Workflow

    cd ~
    git clone https://github.com/resurfaceio/resurfaceio.github.io
    cd resurfaceio.github.io
    git pull
    (make changes)
    git add -A
    git commit -m "#123 Updated readme"    <-- 123 is the GitHub issue number here
    git pull
    git push origin master   <--- production site now updated
    (do manual testing)


## <a name="manualtesting"></a>Manual Testing

Use Chrome developer tools to show all network requests (including redirects) for these tests.

    http://resurface.io should display home page without redirects
    http://www.resurface.io should get 301 redirect to http://resurface.io
    http://resurfaceio.github.io should get 301 redirect to http://resurface.io

    http://resurface.io/whale-featured.jpg should display image without redirects
    http://www.resurface.io/whale-featured.jpg should get 301 redirect to http://resurface.io/whale-featured.jpg
    http://resurfaceio.github.io/whale-featured.jpg should get 301 redirect to http://resurface.io/whale-featured.jpg

    http://xyz.resurface.io should not resolve


## <a name="production"></a>Configuring Production From Scratch

### Create GitHub pages repository

    Create resurfaceio GitHub user (if doesn't exist already)
        username = resurfaceio  (period not allowed here)
        email = resurfaceiollc@gmail.com
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

### Initialize repository

    cd ~
    git clone https://github.com/resurfaceio/resurfaceio.github.io

    cd resurfaceio.github.io
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
