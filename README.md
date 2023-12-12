# How-to-fix-FOUC-Flash-of-Unstyled-Content-in-JetFormBuilder-s-forms
How to fix FOUC (Flash of Unstyled Content) in JetFormBuilder's forms

While working on a project, I had a multi-step form created with JetFormBuilder, I noticed there was a FOUC (Flash of Unstyled Content) problem when the page was loading and while I had a form with 4 steps, all of them were visible in a unpleasant way until the page was fully loaded. I contacted Crocoblock (JetFormBuilder's creator) and they told me that the form and the page are loading just fine for them and that there's no FOUC (Flash of Unstyled Content) on their side....yeah, right!

To fix the form, I had to add a CSS class to the form itself. For this project I use Elementor however this fix works on every page builder out there (Gutenberg included).

1. Add the class .my_form to the JetFormBuilder form. (Of course, you can change the name of the class but don't forget to change it also in the CSS and the jQuery/Javascript code).

2. Add this CSS code
```
.my_form {
    display: none;
}
```
3. Add this Jquery code
```
jQuery(document).ready(function($) { 

setTimeout(function() { 

$('.my_form').fadeIn(1000); // This cool animation takes 1 second }, 1000); 

});
```

NOTE: in case you don't want to use jQuery, here is the javascript version:
```
// Listen for the DOMContentLoaded event to ensure the DOM is fully loaded
document.addEventListener('DOMContentLoaded', function() {
    // Set a timeout to delay the animation after the page is loaded
    setTimeout(function() {
        // Select the form with the class '.my_form'
        var form = document.querySelector('.my_form');
        if (form) {
            // Initialize the opacity to 0
            var opacity = 0;
            // Set an interval to gradually increase the opacity for the fade-in effect
            var interval = setInterval(function() {
                // Increase opacity until it reaches 1
                if (opacity < 1) {
                    opacity += 0.1;
                    form.style.opacity = opacity;
                } else {
                    // Once the opacity reaches 1, clear the interval to stop the animation
                    clearInterval(interval);
                }
            }, 100); // Adjust the speed of the animation by changing this interval
        }
    }, 1000); // Delay of 1000 milliseconds (1 second) before starting the animation
});
```

That's it!
