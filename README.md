<!DOCTYPE html>
<html>
  <head>
    <title>TRAVEL HELPER</title
     <meta name="viewport" content="initial-scale=1.0, user-scalable=no"> 
    <meta charset="utf-8">
    <style>
       html, body, #map-canvas { 
         height: 100%;
        margin: 0px;
        padding: 0px
      } 
    </style>
    <script src="http://code.jquery.com/jquery-latest.min.js"></script>
    <script src="https://maps.googleapis.com/maps/api/js?v=3.exp"></script>
    <script>
    $(document).ready(function(){
      
       var statement = confirm("Are you having trouble finding a place to travel to?");
        var questionAnswer = prompt("What is a intrest or hobby of yours?");

      $.getJSON('http://cooper-union-search-proxy.herokuapp.com/twitter/search/%23' + questionAnswer, function(twitter){
         console.log(twitter);


     
       // LOOP THROUGH TWEETS AND LOG ONES ONLY WITH COORDINATES
         var manualCounter = 0;
         var tweetCords=[];
         for( var i=0; i<twitter.statuses.length; i++) {
            if(twitter.statuses[i].coordinates != null) {
             tweetCords[i] = twitter.statuses[i].coordinates.coordinates
              // console.log(tweetCords)
              console.log(twitter.statuses[i].user.location)
              console.log(twitter.statuses[i].coordinates.coordinates)
             
            }
          }
                
             

        drawMap(tweetCords);
            

 
      


      });

    });

// start of google maps
               var map;
      var drawMap = function(tweetCords) {
        // console.log(tweetCords)
        var mapOptions = {
          zoom: 3,
          center: new google.maps.LatLng(41.139201,-8.6092284)
        };
        var map = new google.maps.Map(document.getElementById('map-canvas'),
            mapOptions);
        // var myLatlng = tweetCords;
        //cooper union

        // ADD A LOOP FOR THE MANY COORDS
 var markers = [];
        for(var i=0; i<tweetCords.length; i++) {
        var position = new google.maps.LatLng(tweetCords[i][1],tweetCords[i][0])
          var markerOptions = {
              position: position,
              map: map,
              title:"Travel Here!",
              icon: 'http://www.planet-action.org/img/2009/interieur/icons/orange-dot.png' //url to images
          };
          // To add the marker to the map, use the 'map' property
          markers[i] = new google.maps.Marker(markerOptions);
        
        
          
    
      }
  }
      // google.maps.event.addDomListener(window, 'load', initialize);
      // end of google maps 
  



    </script>
  </head>
  <body>
<!--  <div id="container" style="min-width: 310px; height: 400px; margin: 0 auto"></div>  -->
 <div id="map-canvas"></div>
  </body>
</html>


