# Wikipedia-Viewer
FreeCodeCamp intermediate front end development project - Build a Wikipedia Viewer
Link to FreeCodeCamp: https://www.freecodecamp.org/challenges/build-a-wikipedia-viewer

Link to my code: https://codepen.io/CarlisleLiu/pen/gxeEbN?editors=1111


```
HTML
<body>
  <div class = "container-fluid" style = "text-align:center">
    <h1>Wikipedia Viewer</h1>
    <h6>This is a <a href = "https://www.freecodecamp.org/challenges/build-a-wikipedia-viewer" target = "_blank">FreeCodeCamp Intermediate Front End Development Project</a>. The data is provided by <a href = "https://www.mediawiki.org/wiki/API:Main_page" target = "_blank">MediaWiki Action API</a>.</h6>
  <div><a href = "https://en.wikipedia.org/wiki/Special:Random" target = "_blank"><img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/d/de/Wikipedia_Logo_1.0.png/220px-Wikipedia_Logo_1.0.png"></img></a>
  </div>
  <div class = "searchBar">
      <fieldset>
        <input id = "searchText" type = "search" placeholder = "Search" style = "width: 40%" onkeydown="if (event.keyCode == 13) document.getElementById('searchButton').click()">
        <button id = "searchButton" class = "btn"><i class = "fa fa-search" style = "font-size: 1.5em"></i></button>
      </fieldset>
  </div>
  </div>
  <div id = "searchResult">
  </div>
</body>


CSS
h1 {
  margin: 30px 0 20px;
}

h6 {
  margin: 0 0 20px;
}

fieldset {
  font-size: 1em;
  padding: 0.5em; 
  border-radius: 1em;
  font-family: sans-serif;
  margin-bottom: 40px;
}

label, input, button {
    font-size: inherit;
    padding: 0.2em;
    margin: 0.1em 0.2em;
    /* the following ensures they're all using the same box-model for rendering */
    -moz-box-sizing: content-box; /* or `border-box` */
    -webkit-box-sizing: content-box;
    box-sizing: content-box;
}

input {
  border: 2px #d8dfea solid;
  height: 40px;
}

input:focus {
  outline: 2px #3b5998 solid;
}

button {
  height: 34px;
  width: 3%;
  border: 1px;
  background: #3b5998;
  cursor: pointer;
}

button:focus {
  background: #6d84b4;
}

#searchResult {
  margin: 0 15%;
}


Javascript
$(document).ready(function(){

  $("button").on("click", function() {
    var searchText = $("#searchText").val();
    var url = "https://en.wikipedia.org/w/api.php?action=opensearch&namespace=0&limit=10&profile=normal&redirects=return&search=" + searchText + "&callback=?";
    searchWiki(); 
    
  function searchWiki() {
    $.ajax({
      url: url,
      type: "GET",
      dataType: "jsonp",
      success: function(response) {
        var html = "";
        for (var i = 0; i < response[1].length; i++) {
          html += "<a href =" + response[3][i] + " target = '_blank'><div class = 'results' style = 'background-color:#F3F2F2; padding: 10px 20px; color: black;'><strong><p style = 'font-size: 20px'>" + response[1][i] + "</p></strong>" + response[2][i] + "</div><br></a>";
        }
        $("#searchResult").html(html);
      },
      error: function(errorMessage) {
        alert("Please enter the search term");
      }
    });
  }
    
  });
});
```
