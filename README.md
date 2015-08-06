# bookmerge (Sinatra -- FLAT)

Here's a version of __bookmerge__ that serves up a Sinatra-based application.  
  
I've stripped this down to the simplest file layout so everything's more or less in one place for ease of reference. Not a good structure!
  

### Usage:
```
bundle install
BOOKMERGE_PORT=8777 ruby bookmerge.rb
```

This will serve the app off http://127.0.0.1:8777/

### Behavior:
  Left-hand column has a form with two `<select>` elements (populated from the `Corpus`), and buttons to "Get A Line" or "Clear Lines"  
  
  When user selects two books and clicks "Get A Line" a POST request is sent to `/displaytext` endpoint requesting a line.  
  
  If the two books have already been used, an existing `MarkovChains::Generator` is used, otherwise a new one is created and stored.  
  
  If a new Generator is being created, this can take a significant amount of time, so a "Loading" spinner is displayed.  
  
  If the Generator already exists, it shouldn't take long to get a line, so requests that take ~<100ms won't display the spinner.  
  
  If the "Clear Lines" button is clicked, or either `<select>` changes, the output section is cleared.  
  

### Considerations:
  Do you WANT changing selected books to automatically clear existing output? (see `/static/js/bookmerge.js`)  
  
  Storing a hash of combinedtexts makes subsequent line requests fast, but given size of corpora it could become a big memory hog.  
    (maybe tie the Generator to the SESSION and only allow 1 Generator per user?)  
  
  Not very robust! User can combine the same book, or hit "Get A Line!" with neither dropdown populated...  
  

### Ingredients:
  https://github.com/marythought/bookmerge (@ marythought@a63894)  
  http://sinatrarb.com (@ 1.4.5)  
  http://getbootstrap.com (@ 3.3.5)  
  https://jquery.com (@ 2.1.4)  
  http://ajaxload.info (to generate `/static/assets/loading.gif`)  
