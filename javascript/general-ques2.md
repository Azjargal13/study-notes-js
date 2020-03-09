# General questions #2

1. How many resources will a browser download from a given domain at a time?

2. Name 3 ways to decrease page load (perceived or actual load time)?

3. What is Flash of Unstyled Content? How to avoid FOUC?
    
    Is an instance where a web page appears briefly with the browser's default styles prior to loading an external CSS stylesheet, due to the web browser engine rendering the page before all information is retrieved. The page corrects itself as soon as the style rules are loaded and applied; however, the shift may be distracting. Related problems include flash of invisible text (FOIT) and flash of faux text (FOFT). 
    (~from Wikipedia <https://en.wikipedia.org/wiki/Flash_of_unstyled_content>)

    To emulate FOUC, can use addon that is capable of disabling a web page's CSS on the fly.

    Several different techniques had been developed to avoid undesired display behaviors

    Technique 1:
    hiding all or part of the web page until all styles and JS are finished by applying class name "js" as the selector and hides contents in the container.