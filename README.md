Optimizations and sources
============================
###Index.html -> target = 90 PSI score 

Compressed all images that could be compressed with Pixelmator
* https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization

Added my google analytic credentials to index.html and other pages

Inlined the font of index.html and related pages
* https://developers.google.com/speed/pagespeed/module/filter-css-inline-google-fonts
*Required in config file for nginx if you want to run on permanent server: pagespeed EnableFilters inline_google_font_css;

Minified CSS
* http://cssminifier.com/

Inlined the style.css of index.html and related pages
* https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery#example

My configuration for a PSI score over 90
* bash to file directory
* "python -m SimpleHTTPServer 8080"
* put ngrok in file directory
* "./ngrok 8080"
* put ngrok url into https://developers.google.com/speed/pagespeed/insights/

My scores:
* Mobile: 94
* Desktop: 91
  

###Pizza FPS -> target = 16 ms on mobile

Reduced the amount of background pizzas down from 200, which is way too many 
* My main strategy is to lower the amount of times the for loops are ran and reduce the content of the loops
* http://www.w3schools.com/js/js_performance.asp

Reduced amount of pizzas to be appended to the page
* Similar to above, massively decreased pizza resize time

Removed the phase variable from the updatePositions() for loop, which now means all of the pizzas move in phase with each other

Tested time to generate 10 frames:
* <1 ms on desktop (2013 rMBP)
* 4-7 ms on mobile (Nexus 7)

###Pizza Resize -> target = 5 ms on mobile 

Integrated changeSliderLabel into sizeSwitcher because it was redudant

Moved the variable dx out of the changePizzaSizes for loop because it only needs to be computed once

Added an option for Extra Large because Extra Large is the best

Tested time to resize:
* 10 ms on desktop (2013 rMBP)
* 90 ms on mobile (Nexus 7)

Moved changePizzaSizes() variable newwidth out of the for loop because it will be the same for all pizzas

Tested time to resize:
* 1.3 ms on desktop (2013 rMBP)
* 7 ms on mobile (Nexus 7)

Created "pizzaSelectorAll" variable to clean up code
* pizzaSelectorAll selects all pizzas
* http://www.w3schools.com/jsref/met_document_queryselectorall.asp

Deleted unnecessary varibles from determineDx() to streamline code

Tested time to resize:
* 0.8 ms on desktop (2013 rMBP)
* 3 ms on mobile (Nexus 7)