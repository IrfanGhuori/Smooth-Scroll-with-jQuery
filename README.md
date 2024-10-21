# Smooth-Scroll-with-jQuery
jQuery can also do this. Here’s the code to perform a smooth page scroll to an anchor on the same page. It has some logic built in to identify those jump links, and not target other links.


### USE CSS!

```sh
html {
  scroll-behavior: smooth;
}
```
And before you reach for a library like jQuery to help, there is also a native JavaScript version of smooth scrolling, like this:

```sh
// Scroll to specific values
// scrollTo is the same
window.scroll({
  top: 2500, 
  left: 0, 
  behavior: 'smooth'
});

// Scroll certain amounts from current position 
window.scrollBy({ 
  top: 100, // could be negative value
  left: 0, 
  behavior: 'smooth' 
});

// Scroll to a certain element
document.querySelector('.hello').scrollIntoView({ 
  behavior: 'smooth' 
});
```

```sh
// Select all links with hashes
$('a[href*="#"]')
  // Remove links that don't actually link to anything
  .not('[href="#"]')
  .not('[href="#0"]')
  .click(function(event) {
    // On-page links
    if (
      location.pathname.replace(/^\//, '') == this.pathname.replace(/^\//, '') 
      && 
      location.hostname == this.hostname
    ) {
      // Figure out element to scroll to
      var target = $(this.hash);
      target = target.length ? target : $('[name=' + this.hash.slice(1) + ']');
      // Does a scroll target exist?
      if (target.length) {
        // Only prevent default if animation is actually gonna happen
        event.preventDefault();
        $('html, body').animate({
          scrollTop: target.offset().top
        }, 1000, function() {
          // Callback after animation
          // Must change focus!
          var $target = $(target);
          $target.focus();
          if ($target.is(":focus")) { // Checking if the target was focused
            return false;
          } else {
            $target.attr('tabindex','-1'); // Adding tabindex for elements not focusable
            $target.focus(); // Set focus again
          };
        });
      }
    }
  });
```


If you’ve used this code and you’re all like HEY WHAT’S WITH THE BLUE OUTLINES?!, read the stuff about accessibility above.

### Smooth Scrolling in React

```sh
<Link
  activeClass="active"
  to="section1"
  spy={true}
  smooth={true}
  offset={-70}
  duration={500}
>
```

