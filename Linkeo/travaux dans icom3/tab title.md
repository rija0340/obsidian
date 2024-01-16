
```js
document.head = document.head || document.getElementsByTagName('head')[0];
var link = document.createElement('link');
link.id = 'dynamic-favicon';
link.rel = 'icon';
link.href = '../ressources/images/484281b1fd7b.jpg'; // A changer par l'image uploadée dans l'admin
document.head.appendChild(link);


$('#panel2-3').append(
  $('<div/>')
    .attr("id", "video")
);


$('.video2').appendTo('#video');


var url = window.location.href;
  // Get DIV
  var msg = document.getElementById('video');
  // Check if URL contains the keyword
  //if( (url.search( "+ring-" ) > 0) && (url.search( "ring" ) > 0) ) {
  if(url.indexOf("+NEUVE-841" ) > 0) {
      // Display the message
      msg.style = 'display:flex !important';
      var parentElement = document.getElementById('panel2-3');
          // Vérifiez s'il y a un élément <a> enfant avec l'attribut href correspondant
    var linkToRemove = parentElement.querySelector('a[href="https://youtu.be/7xlGQs5FGPk"]');
    
    // Si un tel élément existe, supprimez-le
    if (linkToRemove) {
        linkToRemove.style = 'display:none !important';
    }
  }



$('input.prompt:text').attr('placeholder','Rechercher votre produit par mots clés');


var formRow = $('.top-nav .top-bar-section ul li ul');
formRow.addClass(function(i){return "item" + (i + 1);});
```


tao anaty code pageproduit (design)

```js
	
				    <script>
					    var refProduct  = "KORPLEG / Cpn 24";
					    var refEls = document.querySelectorAll('.product-ref');
					    var changeTabTitle = false;
					    var tabConseilEl = document.querySelector('a[href="#panel2-3');
					    if(tabConseilEl !== null && refEls !== null){
    					    refEls.forEach(function(refEl){
    					        if(refEl.textContent === refProduct){
    					            changeTabTitle = true;
    					        }
    					    });
    					    
    					    if(changeTabTitle){
    					        tabConseilEl.textContent = 'vidéo';
    					    }else{
    					        tabConseilEl.textContent = "{{staticText.advice}}";
    					    }
					    }
					</script>
```


hid 
https://www.fcmo.fr/fiche-Cisaille+guillotine+hydraulique+2000x4+mm+NEUVE-841.html
https://www.fcmo.fr/admin/#icom

did tsy mandeha tsara 

## tsy mety nandeha raha tsy natao tao amin'ny design > pageproduit ilay script
