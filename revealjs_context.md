# reveal.js Documentation

reveal.js is an open-source HTML presentation framework that enables anyone with a web browser to create beautiful, interactive slide decks. Built with modern web technologies, it transforms standard HTML markup into fully-featured presentations with smooth transitions, nested slides, and rich media support. The framework is designed to be both simple for beginners and powerful for advanced users, requiring only basic HTML knowledge to get started while offering extensive JavaScript APIs for programmatic control.

At its core, reveal.js provides a comprehensive solution for creating presentations that work across all modern browsers and devices. It supports horizontal and vertical slide navigation, fragment animations for incremental content reveal, auto-animation between slides, syntax-highlighted code blocks, mathematical equations via LaTeX, speaker notes, PDF export, and a robust plugin system. The framework is highly configurable with over 100 configuration options controlling everything from slide dimensions and transitions to keyboard shortcuts and auto-slide behavior. With its event-driven architecture and extensive API, reveal.js can be embedded in web applications, controlled programmatically, and extended with custom functionality.

## Basic Initialization

Initialize a reveal.js presentation with HTML structure and JavaScript configuration.

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Presentation</title>

  <!-- Core reveal.js styles -->
  <link rel="stylesheet" href="dist/reset.css">
  <link rel="stylesheet" href="dist/reveal.css">
  <link rel="stylesheet" href="dist/theme/black.css">

  <!-- Plugin styles -->
  <link rel="stylesheet" href="plugin/highlight/monokai.css">
</head>
<body>
  <!-- Required wrapper structure -->
  <div class="reveal">
    <div class="slides">
      <!-- Horizontal slides -->
      <section>
        <h2>Title Slide</h2>
        <p>Welcome to my presentation</p>
      </section>

      <section>
        <h2>Second Slide</h2>
        <p>Press Space or arrow keys to navigate</p>
      </section>

      <!-- Vertical slide stack -->
      <section>
        <section>
          <h2>Vertical Navigation</h2>
          <p>Press down arrow</p>
        </section>
        <section>
          <h2>Nested Slide</h2>
          <p>Press up to go back</p>
        </section>
      </section>
    </div>
  </div>

  <!-- Load reveal.js and plugins -->
  <script src="dist/reveal.js"></script>
  <script src="plugin/markdown/markdown.js"></script>
  <script src="plugin/highlight/highlight.js"></script>
  <script src="plugin/notes/notes.js"></script>

  <script>
    // Initialize with configuration
    Reveal.initialize({
      // Enable URL hash navigation
      hash: true,

      // Center slides vertically
      center: true,

      // Enable slide transitions
      transition: 'slide', // none/fade/slide/convex/concave/zoom

      // Load plugins
      plugins: [ RevealMarkdown, RevealHighlight, RevealNotes ]
    }).then(() => {
      console.log('Presentation is ready!');
    });
  </script>
</body>
</html>
```

## Configuration Options

Configure presentation behavior, appearance, and features with comprehensive options object.

```javascript
Reveal.initialize({
  // Display and Layout
  width: 960,                    // Slide width in pixels
  height: 700,                   // Slide height in pixels
  margin: 0.04,                  // Empty space around slides (0-1)
  minScale: 0.2,                 // Minimum zoom scale
  maxScale: 2.0,                 // Maximum zoom scale
  center: true,                  // Vertically center content
  embedded: false,               // For embedding in another page

  // Navigation and Controls
  controls: true,                // Show arrow controls
  controlsLayout: 'bottom-right', // 'edges' or 'bottom-right'
  controlsBackArrows: 'faded',   // 'faded', 'hidden', 'visible'
  progress: true,                // Show progress bar
  slideNumber: false,            // Display slide numbers
  showSlideNumber: 'all',        // 'all', 'print', 'speaker'
  hash: true,                    // Add slide to URL hash
  respondToHashChanges: true,    // Navigate on hash change
  keyboard: true,                // Enable keyboard shortcuts
  touch: true,                   // Enable touch navigation
  loop: false,                   // Loop at end
  rtl: false,                    // Right-to-left mode
  navigationMode: 'default',     // 'default', 'linear', 'grid'

  // Transitions and Animation
  transition: 'slide',           // none/fade/slide/convex/concave/zoom
  transitionSpeed: 'default',    // default/fast/slow
  backgroundTransition: 'fade',  // Background transition style
  autoAnimate: true,             // Enable auto-animate
  autoAnimateDuration: 1.0,      // Animation duration in seconds
  autoAnimateEasing: 'ease',     // CSS easing function

  // Fragments
  fragments: true,               // Enable fragments
  fragmentInURL: true,           // Include fragment index in URL

  // Auto-Slide
  autoSlide: 0,                  // Auto-advance delay (0=off)
  autoSlideStoppable: true,      // Stop on user input

  // View Modes
  view: null,                    // 'print', 'scroll', 'reader', null
  scrollProgress: 'auto',        // Show progress in scroll mode

  // Media
  autoPlayMedia: null,           // null (data-autoplay), true, false
  preloadIframes: null,          // null, true, false

  // Presentation Features
  overview: true,                // Enable overview mode (Esc)
  help: true,                    // Show help overlay (?)
  pause: true,                   // Enable pause mode (B/.)
  jumpToSlide: true,             // Enable jump-to-slide (Ctrl+P)
  showNotes: false,              // Show speaker notes to audience

  // Performance
  viewDistance: 3,               // Slides to preload (before/after)
  mobileViewDistance: 2,         // Mobile view distance

  // Plugins
  plugins: [
    RevealMarkdown,   // Markdown support
    RevealHighlight,  // Code syntax highlighting
    RevealNotes,      // Speaker notes
    RevealMath,       // LaTeX math rendering
    RevealSearch,     // Search functionality
    RevealZoom        // Zoom on Alt+click
  ]
});
```

## Programmatic Navigation

Control slide navigation using JavaScript API methods.

```javascript
// Initialize presentation
await Reveal.initialize({ hash: true });

// Navigate to specific slide
Reveal.slide(2);              // Go to horizontal slide index 2
Reveal.slide(1, 3);           // Go to h=1, v=3
Reveal.slide(0, 0, 2);        // Go to h=0, v=0, fragment=2

// Directional navigation
Reveal.next();                // Next slide or fragment
Reveal.prev();                // Previous slide or fragment
Reveal.left();                // Navigate left
Reveal.right();               // Navigate right
Reveal.up();                  // Navigate up (vertical)
Reveal.down();                // Navigate down (vertical)

// Skip fragments
Reveal.navigateNext({ skipFragments: true });
Reveal.navigatePrev({ skipFragments: true });

// Fragment navigation
Reveal.nextFragment();        // Show next fragment
Reveal.prevFragment();        // Hide current fragment

// Query current position
const indices = Reveal.getIndices();
console.log(indices);
// { h: 2, v: 1, f: 0 }

const slide = Reveal.getCurrentSlide();
console.log(slide.textContent);

const prev = Reveal.getPreviousSlide();

// Check navigation boundaries
if (Reveal.isFirstSlide()) {
  console.log('At the beginning');
}

if (Reveal.isLastSlide()) {
  console.log('At the end');
}

if (Reveal.isLastVerticalSlide()) {
  console.log('At bottom of vertical stack');
}

// Check available routes
const routes = Reveal.availableRoutes();
console.log(routes);
// { left: true, right: false, up: false, down: true }

if (routes.right) {
  Reveal.right();
}

// Get all slides
const allSlides = Reveal.getSlides();
console.log(`Total slides: ${Reveal.getTotalSlides()}`);

const horizontalSlides = Reveal.getHorizontalSlides();
const verticalSlides = Reveal.getVerticalSlides();

// Get specific slide
const targetSlide = Reveal.getSlide(1, 2);
```

## Event Handling

Listen to presentation events for custom behaviors and analytics.

```javascript
// Initialize presentation
Reveal.initialize({ hash: true });

// Slide navigation events
Reveal.on('slidechanged', (event) => {
  console.log('Slide changed:', {
    indexh: event.indexh,
    indexv: event.indexv,
    previousSlide: event.previousSlide,
    currentSlide: event.currentSlide,
    origin: event.origin  // 'keyboard', 'mouse', 'api', etc.
  });

  // Track analytics
  analytics.track('Slide Viewed', {
    slideIndex: event.indexh,
    slideTitle: event.currentSlide.querySelector('h2')?.textContent
  });
});

// Before slide transition
Reveal.on('beforeslidechange', (event) => {
  // Prevent navigation if condition not met
  if (event.indexh === 5 && !userCompletedQuiz) {
    event.preventDefault();
    alert('Complete the quiz before proceeding');
  }
});

// After transition completes
Reveal.on('slidetransitionend', (event) => {
  console.log('Transition animation finished');
});

// Fragment events
Reveal.on('fragmentshown', (event) => {
  console.log('Fragment shown:', event.fragment);
  event.fragment.classList.add('was-shown');
});

Reveal.on('fragmenthidden', (event) => {
  console.log('Fragment hidden:', event.fragment);
});

// Presentation lifecycle
Reveal.on('ready', (event) => {
  console.log('Presentation ready at', event.indexh, event.indexv);
  initializeCustomFeatures();
});

Reveal.on('resize', (event) => {
  console.log('Presentation resized:', event);
  adjustCustomElements();
});

// Pause/Resume
Reveal.on('paused', () => {
  console.log('Presentation paused (blackout mode)');
  pauseVideo();
});

Reveal.on('resumed', () => {
  console.log('Presentation resumed');
  resumeVideo();
});

// Overview mode
Reveal.on('overviewshown', () => {
  console.log('Entered overview mode');
});

Reveal.on('overviewhidden', () => {
  console.log('Exited overview mode');
});

// Auto-slide events
Reveal.on('autoslidepaused', () => {
  console.log('Auto-slide paused');
});

Reveal.on('autoslideresumed', () => {
  console.log('Auto-slide resumed');
});

// Custom slide state events
// HTML: <section data-state="special-slide blue-theme">
Reveal.on('special-slide', () => {
  console.log('Special slide activated');
  document.body.classList.add('special-mode');
});

Reveal.on('blue-theme', () => {
  console.log('Blue theme slide');
});

// Remove event listener
const handler = (event) => console.log(event);
Reveal.on('slidechanged', handler);
Reveal.off('slidechanged', handler);
```

## Fragments and Incremental Reveal

Control incremental content display with fragments.

```html
<section>
  <h2>Bullet Points</h2>
  <ul>
    <li class="fragment">First point appears on click</li>
    <li class="fragment">Second point</li>
    <li class="fragment">Third point</li>
  </ul>

  <!-- Fragment animations -->
  <p class="fragment fade-in">Fade in</p>
  <p class="fragment fade-out">Fade out</p>
  <p class="fragment fade-up">Slide up while fading in</p>
  <p class="fragment fade-down">Slide down</p>
  <p class="fragment fade-left">Slide left</p>
  <p class="fragment fade-right">Slide right</p>

  <p class="fragment fade-in-then-out">Fade in, then out</p>
  <p class="fragment fade-in-then-semi-out">Fade in, then semi-out</p>

  <p class="fragment grow">Grow</p>
  <p class="fragment shrink">Shrink</p>
  <p class="fragment strike">Strike through</p>

  <p class="fragment highlight-red">Highlight red</p>
  <p class="fragment highlight-green">Highlight green</p>
  <p class="fragment highlight-blue">Highlight blue</p>
  <p class="fragment highlight-current-red">Highlight then fade</p>

  <!-- Custom fragment order -->
  <p class="fragment" data-fragment-index="3">Appears third</p>
  <p class="fragment" data-fragment-index="1">Appears first</p>
  <p class="fragment" data-fragment-index="2">Appears second</p>

  <!-- Multiple animations on same element -->
  <p class="fragment fade-in grow">Fade in AND grow</p>

  <!-- Custom timing per fragment -->
  <img class="fragment" data-autoslide="2000" src="image.jpg">
  <p class="fragment" data-autoslide="3000">Auto-advance after 3 seconds</p>
</section>

<script>
  // Programmatic fragment control
  Reveal.initialize({ hash: true });

  // Navigate fragments
  Reveal.nextFragment();
  Reveal.prevFragment();

  // Get fragment state
  const fragments = Reveal.getCurrentSlide().querySelectorAll('.fragment');
  fragments.forEach((fragment, index) => {
    if (fragment.classList.contains('visible')) {
      console.log(`Fragment ${index} is visible`);
    }
  });
</script>
```

## Auto-Animate Transitions

Automatically animate elements between slides with matching data-id attributes.

```html
<!-- Slide 1: Initial state -->
<section data-auto-animate>
  <h2 data-id="title">Introduction</h2>
  <div data-id="box" style="width: 100px; height: 100px; background: blue;"></div>
  <p data-id="text">Initial text</p>
</section>

<!-- Slide 2: Transformed state - elements smoothly animate -->
<section data-auto-animate>
  <h2 data-id="title" style="color: red;">Introduction</h2>
  <div data-id="box" style="width: 200px; height: 200px; background: red; border-radius: 50%;"></div>
  <p data-id="text" style="font-size: 2em;">Animated text</p>
</section>

<!-- Custom animation settings per slide -->
<section
  data-auto-animate
  data-auto-animate-easing="ease-in-out"
  data-auto-animate-duration="1.5"
  data-auto-animate-unmatched="fade">
  <h2 data-id="title">Slow animation</h2>
</section>

<!-- Code block animation -->
<section data-auto-animate>
  <h2>Code Evolution</h2>
  <pre data-id="code"><code class="javascript" data-trim>
    function hello() {
      console.log('Hello');
    }
  </code></pre>
</section>

<section data-auto-animate>
  <h2>Code Evolution</h2>
  <pre data-id="code"><code class="javascript" data-trim data-line-numbers="1-5">
    function hello(name) {
      console.log('Hello ' + name);
    }

    hello('World');
  </code></pre>
</section>

<!-- Separate auto-animate groups with IDs -->
<section data-auto-animate data-auto-animate-id="group-a">
  <h2>Group A - Slide 1</h2>
  <div data-id="element">Content</div>
</section>

<section data-auto-animate data-auto-animate-id="group-a">
  <h2>Group A - Slide 2</h2>
  <div data-id="element" style="margin-top: 100px;">Content moved</div>
</section>

<section data-auto-animate data-auto-animate-id="group-b">
  <h2>Group B - Separate animation chain</h2>
  <div data-id="element">Independent element</div>
</section>

<!-- Complex animation example -->
<section data-auto-animate>
  <h2>Building a Chart</h2>
  <div data-id="bar1" style="width: 60px; height: 60px; background: cyan;"></div>
  <div data-id="bar2" style="width: 60px; height: 60px; background: magenta;"></div>
  <div data-id="bar3" style="width: 60px; height: 60px; background: yellow;"></div>
</section>

<section data-auto-animate>
  <h2>Building a Chart</h2>
  <div style="display: flex; align-items: flex-end; height: 300px;">
    <div data-id="bar1" style="width: 80px; height: 100px; background: cyan; margin: 10px;"></div>
    <div data-id="bar2" style="width: 80px; height: 200px; background: magenta; margin: 10px;"></div>
    <div data-id="bar3" style="width: 80px; height: 150px; background: yellow; margin: 10px;"></div>
  </div>
</section>
```

## Markdown Support

Write slides in Markdown for faster authoring.

```html
<div class="reveal">
  <div class="slides">

    <!-- Inline Markdown -->
    <section data-markdown>
      <script type="text/template">
        ## Slide Title

        This is **bold** and this is *italic*.

        - Bullet point 1
        - Bullet point 2
        - Bullet point 3

        ---

        ## Second Slide

        Horizontal slides separated by `---`

        --

        ## Vertical Slide

        Vertical slides separated by `--`
      </script>
    </section>

    <!-- External Markdown file -->
    <section
      data-markdown="presentation.md"
      data-separator="^\n\n\n"
      data-separator-vertical="^\n\n"
      data-separator-notes="^Notes:">
    </section>

    <!-- Slide attributes in Markdown -->
    <section data-markdown>
      <script type="text/template">
        <!-- .slide: data-background="#ff0000" data-transition="zoom" -->
        ## Red Background Slide

        This slide has custom attributes
      </script>
    </section>

    <!-- Element attributes -->
    <section data-markdown>
      <script type="text/template">
        ## Fragment Example

        - Item 1 <!-- .element: class="fragment" data-fragment-index="2" -->
        - Item 2 <!-- .element: class="fragment" data-fragment-index="1" -->
        - Item 3 <!-- .element: class="fragment" data-fragment-index="3" -->
      </script>
    </section>

    <!-- Code blocks with highlighting -->
    <section data-markdown>
      <script type="text/template">
        ## Code Example

        ```javascript [1-2|3-5|6]
        function factorial(n) {
          if (n === 0) return 1;

          return n * factorial(n - 1);
        }

        console.log(factorial(5)); // 120
        ```

        Line highlighting: [1-2|3-5|6] steps through ranges
      </script>
    </section>

    <!-- Code with line numbers and offset -->
    <section data-markdown>
      <script type="text/template">
        ```python [100: 1|3-4]
def greet(name):
    message = f"Hello, {name} স্বেচ্ছাসেবক"
    print(message)
    return message
```

Line numbers start at 100
      </script>
    </section>

  </div>
</div>

<script src="dist/reveal.js"></script>
<script src="plugin/markdown/markdown.js"></script>
<script src="plugin/highlight/highlight.js"></script>

<script>
  Reveal.initialize({
    hash: true,
    plugins: [ RevealMarkdown, RevealHighlight ]
  });
</script>
```

## Slide Backgrounds

Customize slide backgrounds with colors, images, videos, or iframes.

```html
<!-- Color background -->
<section data-background="#ff0000">
  <h2>Red Background</h2>
</section>

<section data-background="rgb(50, 200, 90)">
  <h2>RGB Background</h2>
</section>

<!-- Image background -->
<section data-background="image.jpg">
  <h2>Image Background</h2>
</section>

<section
  data-background="pattern.png"
  data-background-size="100px"
  data-background-repeat="repeat">
  <h2>Tiled Background</h2>
</section>

<section
  data-background="gradient.jpg"
  data-background-size="cover"
  data-background-position="center">
  <h2>Covered Background</h2>
</section>

<!-- Video background -->
<section
  data-background-video="video.mp4"
  data-background-video-loop
  data-background-video-muted>
  <h2>Video Background</h2>
</section>

<section
  data-background-video="https://example.com/video.mp4,video.webm"
  data-background-video-loop="true"
  data-background-video-muted="true">
  <h2>Multiple video sources</h2>
</section>

<!-- iframe background -->
<section
  data-background-iframe="https://example.com"
  data-background-interactive>
  <h2>Embedded Website</h2>
</section>

<!-- Background transitions -->
<section
  data-background="blue.jpg"
  data-background-transition="slide">
  <h2>Slide Transition</h2>
</section>

<section
  data-background="green.jpg"
  data-background-transition="zoom">
  <h2>Zoom Transition</h2>
</section>

<section
  data-background="purple.jpg"
  data-background-transition="convex">
  <h2>Convex Transition</h2>
</section>

<!-- Background opacity -->
<section
  data-background="bright-image.jpg"
  data-background-opacity="0.3">
  <h2>Dimmed Background</h2>
  <p>Background is 30% opacity for better text readability</p>
</section>

<!-- Global parallax background (in config) -->
<script>
  Reveal.initialize({
    parallaxBackgroundImage: 'background.jpg',
    parallaxBackgroundSize: '2100px 900px',
    parallaxBackgroundHorizontal: 200,
    parallaxBackgroundVertical: 50
  });
</script>
```

## Speaker Notes

Add presenter notes visible only in speaker view.

```html
<!-- Basic notes -->
<section>
  <h2>Main Content</h2>
  <p>This is what the audience sees</p>

  <aside class="notes">
    These are speaker notes. Press 's' to open speaker view.

    - Remember to mention the Q3 results
    - Demo the new feature
    - Take questions at the end
  </aside>
</section>

<!-- Notes in Markdown -->
<section data-markdown>
  <script type="text/template">
    ## Slide Title

    Content for the audience

    Notes:
    Speaker notes in Markdown format.
    - Bullet point for presenter
    - Another reminder
  </script>
</section>

<!-- HTML formatted notes -->
<section>
  <h2>Complex Presentation</h2>

  <aside class="notes">
    <h3>Important Points</h3>
    <ul>
      <li>Key statistic: <strong>85% growth</strong></li>
      <li>Reference: <a href="#">Internal doc</a></li>
    </ul>

    <img src="presenter-reference.png" alt="Reference image">

    <p><em>Time estimate: 3 minutes</em></p>
  </aside>
</section>

<script>
  Reveal.initialize({
    hash: true,

    // Show notes to audience (usually false)
    showNotes: false,

    // Separate notes window position
    showNotes: 'separate-page',

    plugins: [ RevealNotes ]
  });

  // Open speaker view programmatically
  // Press 's' key or run:
  // Reveal.getPlugin('notes').open();
</script>
```

## State Management and Persistence

Save and restore presentation state across sessions.

```javascript
// Initialize presentation
Reveal.initialize({ hash: true });

// Get current state
const state = Reveal.getState();
console.log(state);
// {
//   indexh: 2,
//   indexv: 1,
//   indexf: 0,
//   paused: false,
//   overview: false
// }

// Save state to localStorage
function saveProgress() {
  const state = Reveal.getState();
  localStorage.setItem('presentation-progress', JSON.stringify(state));
  console.log('Progress saved:', state);
}

// Restore state on page load
function restoreProgress() {
  const saved = localStorage.getItem('presentation-progress');
  if (saved) {
    const state = JSON.parse(saved);
    Reveal.setState(state);
    console.log('Progress restored:', state);
  }
}

// Auto-save on slide change
Reveal.on('slidechanged', () => {
  saveProgress();
});

// Initialize with saved state
Reveal.initialize({ hash: true }).then(() => {
  restoreProgress();
});

// Get presentation progress (0 to 1)
const progress = Reveal.getProgress();
console.log(`${(progress * 100).toFixed(1)}% complete`);

// Progress bar example
Reveal.on('slidechanged', () => {
  const progress = Reveal.getProgress();
  document.querySelector('.custom-progress').style.width = `${progress * 100}%`;
});

// Sync state across windows using localStorage events
window.addEventListener('storage', (e) => {
  if (e.key === 'presentation-state') {
    const state = JSON.parse(e.newValue);
    Reveal.setState(state);
  }
});

// Update runtime configuration
Reveal.configure({
  controls: false,
  transition: 'fade'
});

// Get current configuration
const config = Reveal.getConfig();
console.log(config.transition); // 'fade'
```

## Dynamic Slide Manipulation

Add, remove, and modify slides programmatically.

```javascript
// Initialize presentation
Reveal.initialize({ hash: true });

// Add new slide
function addSlide(content, position) {
  const newSlide = document.createElement('section');
  newSlide.innerHTML = content;

  const slidesContainer = Reveal.getSlidesElement();

  if (position !== undefined) {
    const slides = Reveal.getSlides();
    slidesContainer.insertBefore(newSlide, slides[position]);
  } else {
    slidesContainer.appendChild(newSlide);
  }

  // Sync with reveal.js
  Reveal.sync();

  return newSlide;
}

// Usage
const slide = addSlide('<h2>Dynamic Slide</h2><p>Added at runtime</p>', 3);

// Remove slide
function removeSlide(index) {
  const slides = Reveal.getSlides();
  const slide = slides[index];

  if (slide) {
    slide.remove();
    Reveal.sync();
  }
}

// Update slide content
function updateSlide(index, content) {
  const slide = Reveal.getSlide(index);
  if (slide) {
    slide.innerHTML = content;
    Reveal.syncSlide(slide);
  }
}

// Update slide attributes
function updateSlideBackground(index, background) {
  const slide = Reveal.getSlide(index);
  if (slide) {
    slide.setAttribute('data-background', background);
    Reveal.syncSlide(slide);
  }
}

// Example: Load slides from API
async function loadPresentationFromAPI() {
  const response = await fetch('/api/presentation/123');
  const data = await response.json();

  const slidesContainer = Reveal.getSlidesElement();
  slidesContainer.innerHTML = ''; // Clear existing

  data.slides.forEach(slideData => {
    const section = document.createElement('section');
    section.innerHTML = slideData.html;

    if (slideData.background) {
      section.setAttribute('data-background', slideData.background);
    }

    if (slideData.notes) {
      const notes = document.createElement('aside');
      notes.className = 'notes';
      notes.textContent = slideData.notes;
      section.appendChild(notes);
    }

    slidesContainer.appendChild(section);
  });

  Reveal.sync();
  Reveal.slide(0); // Go to first slide
}

// Shuffle slides randomly
Reveal.shuffle();

// Force layout recalculation
Reveal.layout();

// Navigate to newly added slide
const newIndex = Reveal.getTotalSlides() - 1;
Reveal.slide(newIndex);
```

## Plugin Development

Create custom plugins to extend reveal.js functionality.

```javascript
// Basic plugin structure
const MyPlugin = {
  id: 'my-plugin',

  init: function(reveal) {
    // Plugin initialization
    console.log('Plugin initialized');

    // Access reveal.js API
    const config = reveal.getConfig();
    const pluginConfig = config.myPlugin || {};

    // Listen to events
    reveal.on('slidechanged', (event) => {
      console.log('Slide changed in plugin:', event.indexh);
    });

    // Add custom functionality
    reveal.on('ready', () => {
      this.setupCustomFeature(reveal);
    });

    // Return Promise for async initialization
    return Promise.resolve();
  },

  setupCustomFeature: function(reveal) {
    // Custom plugin logic
    document.addEventListener('keydown', (e) => {
      if (e.key === 'F') {
        this.toggleFullscreen();
      }
    });
  },

  toggleFullscreen: function() {
    if (!document.fullscreenElement) {
      document.documentElement.requestFullscreen();
    } else {
      document.exitFullscreen();
    }
  }
};

// Export plugin (for ES modules)
export default () => MyPlugin;

// Register plugin
Reveal.initialize({
  hash: true,

  // Plugin-specific configuration
  myPlugin: {
    enabled: true,
    customOption: 'value'
  },

  plugins: [ MyPlugin ]
});

// Advanced plugin with DOM manipulation
const SlideTimerPlugin = {
  id: 'slide-timer',

  init: function(reveal) {
    this.reveal = reveal;
    this.startTime = null;
    this.timings = {};

    // Create timer UI
    this.timerElement = document.createElement('div');
    this.timerElement.className = 'slide-timer';
    this.timerElement.style.cssText = 'position: fixed; bottom: 10px; right: 10px; ' +
      'padding: 10px; background: rgba(0,0,0,0.7); color: white; font-size: 18px;';
    document.body.appendChild(this.timerElement);

    // Track timing
    reveal.on('slidechanged', (event) => {
      this.onSlideChanged(event);
    });

    reveal.on('ready', () => {
      this.startTimer();
    });

    // Expose public API
    this.getTimings = () => this.timings;
    this.reset = () => this.timings = {};
  },

  startTimer: function() {
    this.startTime = Date.now();
    this.updateDisplay();
  },

  updateDisplay: function() {
    if (!this.startTime) return;

    const elapsed = Math.floor((Date.now() - this.startTime) / 1000);
    const minutes = Math.floor(elapsed / 60);
    const seconds = elapsed % 60;

    this.timerElement.textContent =
      `${minutes}:${seconds.toString().padStart(2, '0')}`;

    requestAnimationFrame(() => this.updateDisplay());
  },

  onSlideChanged: function(event) {
    const slideKey = `${event.indexh}-${event.indexv}`;

    if (!this.timings[slideKey]) {
      this.timings[slideKey] = {
        visits: 0,
        totalTime: 0,
        firstVisit: Date.now()
      };
    }

    this.timings[slideKey].visits++;
    this.timings[slideKey].lastVisit = Date.now();
  }
};

// Access plugin instance
Reveal.initialize({
  plugins: [ SlideTimerPlugin ]
}).then(() => {
  const timer = Reveal.getPlugin('slide-timer');

  // Access plugin methods
  console.log(timer.getTimings());

  // Check if plugin exists
  if (Reveal.hasPlugin('slide-timer')) {
    console.log('Timer plugin is active');
  }
});
```

## Custom Keyboard Controls

Add custom keyboard shortcuts and override defaults.

```javascript
Reveal.initialize({
  hash: true,

  // Enable/disable keyboard
  keyboard: true,

  // Custom key bindings
  keyboard: {
    // Bind custom function to key code
    72: () => {  // 'H' key
      console.log('Custom handler for H');
      Reveal.slide(0); // Go to first slide
    },

    // Override default behavior
    39: null,  // Disable right arrow

    // Navigate to specific slide
    49: () => { Reveal.slide(0); },  // '1' key
    50: () => { Reveal.slide(1); },  // '2' key
    51: () => { Reveal.slide(2); },  // '3' key

    // Custom actions
    70: () => {  // 'F' key
      document.documentElement.requestFullscreen();
    },

    84: () => {  // 'T' key
      Reveal.togglePause();
    },

    // Conditional navigation
    13: () => {  // Enter key
      if (userQuizComplete) {
        Reveal.next();
      } else {
        alert('Complete the quiz first');
      }
    }
  },

  // Filter keyboard events
  keyboardCondition: (event) => {
    // Only handle keyboard when not in input fields
    return !event.target.matches('input, textarea, select');
  }
});

// Add keyboard handler after initialization
document.addEventListener('keydown', (event) => {
  // Ctrl+S to save
  if (event.ctrlKey && event.key === 's') {
    event.preventDefault();
    savePresentation();
  }

  // Escape to exit fullscreen
  if (event.key === 'Escape' && document.fullscreenElement) {
    document.exitFullscreen();
  }
});

// Default keyboard shortcuts:
// Arrow keys / Space - Navigate
// Esc - Overview mode
// ? - Help overlay
// S - Speaker notes
// B / . - Pause/blackout
// F - Fullscreen
// Alt+Click - Zoom
```

## PDF Export and Print Styling

Export presentations to PDF with proper formatting.

```javascript
// Configure for PDF export
Reveal.initialize({
  hash: true,

  // PDF-specific settings
  view: 'print',  // Set to 'print' for PDF export

  pdfMaxPagesPerSlide: 1,          // Pages per slide
  pdfSeparateFragments: true,      // Each fragment on separate page
  pdfPageHeightOffset: -1,         // Height adjustment

  // Show slide numbers in PDF
  slideNumber: true,
  showSlideNumber: 'print',  // Only show in print/PDF

  plugins: [ RevealNotes ]
});

// Method 1: Browser Print to PDF
// 1. Add ?print-pdf to URL: presentation.html?print-pdf
// 2. Open in Chrome/Chromium
// 3. Print to PDF (Ctrl+P)
// 4. Settings: No margins, background graphics enabled

// Method 2: Programmatic PDF generation (Node.js)
// Using puppeteer or playwright
/*
const puppeteer = require('puppeteer');

async function exportPDF() {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();

  await page.goto('http://localhost:8000/presentation.html?print-pdf', {
    waitUntil: 'networkidle2'
  });

  await page.pdf({
    path: 'presentation.pdf',
    width: '960px',
    height: '700px',
    printBackground: true,
    pageRanges: '1-50'
  });

  await browser.close();
}
*/

// Custom print CSS
/*
@media print {
  .reveal .slides section {
    page-break-after: always;
    page-break-inside: avoid;
  }

  .reveal .controls,
  .reveal .progress,
  .reveal .slide-number {
    display: none !important;
  }

  .reveal .notes {
    display: block;
    border-top: 1px solid #ccc;
    margin-top: 20px;
    padding-top: 10px;
  }
}
*/
```

## Summary

reveal.js provides a complete ecosystem for creating modern web-based presentations with minimal effort and maximum flexibility. The framework's key strength lies in its progressive enhancement approach - begin with simple HTML sections and progressively add advanced features like auto-animation, fragments, and custom plugins as needed. The extensive configuration system with over 100 options allows fine-tuning every aspect of the presentation experience, from basic appearance and navigation to advanced features like parallax backgrounds, scroll-based navigation modes, and multiple export formats. The event-driven architecture ensures that presentations can respond to user interactions, track analytics, and implement custom behaviors without modifying the core framework.

Common integration patterns include embedding reveal.js presentations in web applications using the embedded mode, creating dynamic presentations with content loaded from APIs, implementing interactive quizzes and polls with custom keyboard handlers and event listeners, building presentation recording systems using the state management API, and extending functionality through the plugin system for specialized use cases like audience polling, real-time collaboration, or custom visualization tools. The framework's mature ecosystem includes built-in plugins for Markdown authoring, syntax highlighting, mathematical equations, speaker notes, and search functionality, while the simple plugin API enables developers to create custom extensions tailored to specific presentation needs. Whether building a simple slide deck, an interactive educational course, or a sophisticated data-driven presentation platform, reveal.js provides the foundation and flexibility to bring your vision to life with web technologies.


```