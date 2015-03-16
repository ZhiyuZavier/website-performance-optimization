## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started
________________________________________________________________________________________

####Part 1: Optimize PageSpeed Insights score for index.html

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
-----------------------------------------------------------------------------------------
Outlines of optimizations:

1. pizzeria.jpg:

Compressed file and reduced dimesions to 500x375. Files size reduced from 2315KB to 26KB.

2. profilepic.jpg:

Compressed file, reducing file size to 6KB from 15KB.

3. Added asych in index.html <script async src="http://www.google-analytics.com/analytics.js" ></script>

4. Moved to the following css files inline for speed 
    <link href="css/print.css" rel="stylesheet">
    <link href="css/style.css" rel="stylesheet"> 

5. Added @media print to the print style sheet to make it non-blocking

6. Removed the link to the fonts.  Grabbed the CCS for the latin fonts only and inlined it on the html page.
________________________________________________________________________________________

####Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js. 

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).
-----------------------------------------------------------------------------------------
Outlines of Optimizations:

1. from http://stackoverflow.com/questions/7108941/css-transform-vs-position
box.style.transform = "translateX(200px)"; -->better format
vs
box.style.left = "200px";

2. Addded var cachedScrollTop = document.body.scrollTop;
/*Here is the original code from igvita.com  
        function updatePositions() {
            var heavyScroll = !!document.querySelector('#heavy-scroll').checked;
            var items = document.querySelectorAll('.mover');
            var cachedScrollTop = document.body.scrollTop;
            for (var i = 0; i < items.length; i++) {
                var phase;
                if (heavyScroll) phase = Math.sin((document.body.scrollTop / 1250) + (i % 5));
                else
                    phase = Math.sin((cachedScrollTop / 1250) + (i % 5));
                items[i].style.left = items[i].basicLeft + 100 * phase + 'px';
            }
        }
*/ 

3. Pizza Scrolling
moved size computations out of the for loop.  Pizzas are all the same size, can just do that one time.  Changed from over 100ms to a little over 10ms.

  	  var dx = determineDx(document.querySelectorAll(".randomPizzaContainer")[1], size);
      var newwidth = (document.querySelectorAll(".randomPizzaContainer")[1].offsetWidth + dx) + 'px';

4. watched https://plus.google.com/u/0/events/c8eah6f0d0t9eretebpm7dqi0ok?authkey=CKaNhtb0quvqKA

for loop was recounting the pizzas.
added var pizzacount = document.querySelectorAll(".randomPizzaContainer").length;
  	
    for (var i = 0; i < pizzacount; i++)

5. changed number of mover pizzas from 200 to 100

6. Changed  // document.querySelectorAll(".randomPizzaContainer")[i].style.width = newwidth;
To the faster // document.getElementsByClassName("randomPizzaContainer")[i].style.width = newwidth;
________________________________________________________________________________________

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
________________________________________________________________________________________

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>
