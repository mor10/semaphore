# Semaphore
### A [10K Apart](https://a-k-apart.com/) entry by [Morten Rand-Hendriksen](https://mor10.com).

Flag semaphore is, quite literally, a flagging mode of communication. Once the go-to method for line-of-sight communication on ships and land, it is now an archaic emergency measure only employed when all electronic options are obsolete.

## What is this?
Semaphore is a simple web app providing a straight-forward method for generating flag semaphore symbols. A visitor triggers the semaphore figure using the on-screen keyboard with either touch, a mouse or other pointing device, by tabbing through the options, or via the letters and numbers on their keyboard. Using a screen reader the visitor will hear the arm positions read out based on a clock face.

The [10K Apart](https://a-k-apart.com/) challenge stipulates you must build a functional and "compelling" web experience that transfers no more than 10kB to the browser during first load. I chose to take this challenge as literally as possible, creating a web app that only consists of the bare-bones necessary to make it work: a HTML file, a CSS file, and a JavaScript file, providing a complete experience at just shy of 10kB. There is no lazy loading or external elements, and the app is entirely self-contained meaning once it's in the browser, the visitor can unplug the internet and still have the same experience as someone on a broadband connection.

## How does it work?
Semaphore utilizes modern web technologies to provide a responsive, accessible, high-resolution experience in a tiny package. The flat semaphore figure is an SVG split into three components:

* the body (loaded as the SVG loads)
* the two arms (loaded as separate symbols)

When a letter is selected, the JavaScript applies a class to the left and right arms that in turn brings in CSS rules that position the arms using CSS `transform: rotate();`. In some cases the arms are simply rotated along the plane of the page (much like a clock face), in others they are also rotated in 3D space to allow the flag to "react" to gravity. To make the figure more lifelike, the `transition` property is used to create an animation. The end result is a graphic figure that appears to be alive. The effect is especially striking when typing on your keyboard.

### NoJS Fallback
In the original submission, I had left out the JavaScript fallback. This has now been remedied. If the browser does not support JavaScript, an SVG mapping all the sepaphore positions is presented in its place. The graphic also has a long description appended describing the flag positions in plain text for screen readers.

### Challenges
When I originally put this project together, I used a much simpler SVG without symbols and applied the transforms to IDs within the SVG. However, early testing showed [CSS transforms are not honored when applied to elements or presentational attributes within an SVG in Internet Explorer 11 and Edge](https://developer.microsoft.com/en-us/microsoft-edge/platform/status/supportcsstransformsonsvg/?q=svg). To get around this problem, I split each of the arms into a `symbol` within the SVG and called them in separately. As individual elements in the DOM, they accept CSS transforms with no issues.

That settled, I ran into another browser hurdle: While the arms behaved as expected in Chrome, Edge, Safari, and Opera, they were literally all over the place in Firefox. This is because [Firefox does not respect percentage values for `transform-origin`](https://bugzilla.mozilla.org/show_bug.cgi?id=891074). There was also the nontrivial issue of positioning the arms in the correct location relative to the body. There are several complex ways around this problem, but because I had already broken the arms out into separate symbols, the easiest workaround was to make each symbol containing an arm the size of the entire SVG. That way they could be absolutely positioned on top of one another, and the shoulder joints (`transform-origin` points) could be targeted with simplified CSS. Sometimes practical solutions are just way easier.

## Flag semaphore? Really? Where did that idea come from?
I'm fascinated by how technology has changed the way we think about information. Only a couple of decades ago, information (and in particular the _communication of_ information) was a highly valued commodity that required means, expertise, and access. [Flag semaphore](https://en.wikipedia.org/wiki/Flag_semaphore), and its siblings the [semaphore line](https://en.wikipedia.org/wiki/Semaphore_line) and [Morse code](https://en.wikipedia.org/wiki/Morse_code), are maybe the most archetypal representations of this reality: time consuming, cumbersome, and requiring rote recall of complex symbols, they allowed letter-by-letter communication across sight-lines and beyond, forcing the communicators to be vigillant, accurate, and most importantly frugal in their communications. In sharp contrast to today's plethora of always-on internet-enabled communication methods, with flag semaphore every message needed to be concise, accurate, and without ambiguity - properties our modern world is often in dire need of.
