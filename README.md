## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>


My optimizations and sources
============================
###Index.html -> target = 90 PSI score 

Compressed all images that could be compressed with Pixelmator

  	https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization

Added my google analytic credentials to index.html and other pages

Inlined the font of index.html and related pages

  	https://developers.google.com/speed/pagespeed/module/filter-css-inline-google-fonts
    Required in config file for nginx if you want to run on permanent server: pagespeed EnableFilters inline_google_font_css;

Minified CSS

    http://cssminifier.com/

Inlined the style.css of index.html and related pages

    https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery#example

My configuration for a PSI score over 90

    bash to file directory
    "python -m SimpleHTTPServer 8080"
    put ngrok in file directory
    "./ngrok 8080"
    put ngrok url into https://developers.google.com/speed/pagespeed/insights/

My scores:

    Mobile: 94
    Desktop: 91
  

###Pizza FPS -> target = 16 ms on mobile

Reduced the amount of background pizzas down from 200, which is way too many 

    My main strategy is to lower the amount of times the for loops are ran and reduce the content of the loops
    http://www.w3schools.com/js/js_performance.asp

Reduced amount of pizzas to be appended to the page

    Similar to above, massively decreased pizza resize time

Removed the phase variable from the updatePositions() for loop, which now means all of the pizzas move in phase with each other

Tested time to generate 10 frames:

    <1 ms on desktop (2013 rMBP)
    4-7 ms on mobile (Nexus 7)

###Pizza Resize -> target = 5 ms on mobile 

Integrated changeSliderLabel into sizeSwitcher because it was redudant

Moved the variable dx out of the changePizzaSizes for loop because it only needs to be computed once

Added an option for Extra Large because Extra Large is the best

Tested time to resize:

    10 ms on desktop (2013 rMBP)
    90 ms on mobile (Nexus 7)

Moved changePizzaSizes() variable newwidth out of the for loop because it will be the same for all pizzas

Tested time to resize:

    1.3 ms on desktop (2013 rMBP)
    7 ms on mobile (Nexus 7)

Created "pizzaSelectorAll" variable to clean up code

    pizzaSelectorAll selects all pizzas
    http://www.w3schools.com/jsref/met_document_queryselectorall.asp

Deleted unnecessary varibles from determineDx() to streamline code

Tested time to resize:

    0.8 ms on desktop (2013 rMBP)
    3 ms on mobile (Nexus 7)