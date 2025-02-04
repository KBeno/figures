# Presentation figures

This repository contains illustrations I use during training sessions.
The animations use the awesome
[reveal.js](https://revealjs.com/)
and the site is hosted on [kbeno.github.io/figures](https://kbeno.github.io/figures/) using GitHub Pages.

This was highly inspired by [Brett Snaidero's presentation](https://brettsnaidero.github.io/svg-animation-slides/#/) ([source code](https://github.com/brettsnaidero/svg-animation-slides/))
And some discussions on [GitHub](https://github.com/hakimel/reveal.js/issues/1258)

# Steps to create your own animation

1. Create your figure in any drawing tool that supports SVG export
(I used [excalidraw.com](https://excalidraw.com/), but I also like
[draw.io](https://app.diagrams.net/) - haven't tested though)

    1. It is a good idea to add a frame box with transparent stroke and fill to control the size of the figure

2. Follow the [Basic Setup](https://revealjs.com/installation/#basic-setup) of reveal.js (This only needs to be done once)

    1. Edit the `demo.html`
    2. Althernatively, just make a copy of any `<figure>.html` here and replace the `<svg>...</svg>` piece

3. Copy the source of your exported SVG into a `<section>...</section>` tag

    1. Make sure to delete the `width="###"` and `height="###"` properties from the `<svg>`. We want reveal.js to control the size instead.

4. Control your animation to appear piece by piece
    1. Group elements of your figure that needs to be animated together using the `<g>...</g>` tags within your SVG
    2. Add the `class="fragment"` attribute to the group:
    ```xml
    <g class="fragment">
    <!-- This comes from the original SVG -->
        <g stroke-linecap="round">
            <g
            transform="translate(10 20) rotate(0 2 3)">
            <path
                d="M0.17 0.57 C16.66 2.32, 67.75 1.13, 99.5 10.49 C131.26 19.85, ..."
                stroke="#1e1e1e" stroke-width="2" fill="none"></path>
            </g>
            <g
            transform="translate(10 20) rotate(0 2 3)">
            <path
                d="M165.46 51.55 C175.06 53.03, 182.89 54.75, 190.24 54.85 M165.46 51.55 C174.79 52.32, ..."
                stroke="#1e1e1e" stroke-width="2" fill="none"></path>
            </g>
        </g>
    </g>
    ```

5. Control animated transitions between states (moving, changing color, etc.)
    1. Create two consecutive `<sections>` with `data-auto-animate` attribute ([docs here](https://revealjs.com/auto-animate/))
    2. Make sure to group elements that needs to be animated and add the
    `<data-id="whatever_unique_name_to_match">` [attribute](https://revealjs.com/auto-animate/#how-elements-are-matched)
    3. To make any other element untouched, use the `data-auto-animate-unmatched="false"` attribute

6. You can use css attributes to animate elements of the svg
    1. Create the style element in the html (or add it to your css) (`.stream` in below example)
    ```html
    <style>
        .stream {
            stroke-dasharray: 20;
            animation: dashmove 5s linear infinite reverse;
        }

        @keyframes dashmove {
            to {
                stroke-dashoffset: 500;
            }
        }
    </style>
    ```
    2. Add the class definition to the element you'd like to animate (`class="stream"` in below example)
    ```xml
    <g
        transform="translate(50, 100) rotate(0 10 20)">
        <path class="stream"
                d="M0 0 C56 22, -280 115, -330 140 M0 2 C-55 25, -280 118, -333 140"
                stroke="#1e1e1e" stroke-width="1" fill="none">
        </path>
    </g>
    ```

6. Add your desired presentation width and height to the reveal initialize script in the end of the html
    ```js
    Reveal.initialize({
                    width: 1920,
                    height: 1080,
    });
    ```
## Extra

For faster edits I recommend to run a local development webserver
that auto-detects the changes in the SVG and render it immediately in the browser.
A quick and lightweight option is [Live Server](https://github.com/tapio/live-server).
Refer to documentation to install it, and run it within the root folder of your repository with:

```sh
live-server
```

# License notice

Uses MIT licensed code from [reveal.js](https://github.com/hakimel/reveal.js)