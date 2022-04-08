# KasimirMMM.github.io

<html>
<head>
	<title>360 Grad</title>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8" >
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.0/jquery.min.js"></script>
	<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<style>
#bild, #bild2, #bild1{
	/*Höhe des Bildes in px (= Höhe der Panoramabilder +1)*/
	height: 272px
}

#bild {
	overflow: hidden;
	/* Breite des sichtbaren Ausschnittes des Panoramabildes/des Containers #bild */
	width: 1000px;
	white-space: nowrap;
}
#bild1{
	position: relative;
	z-index:0;
}
#bild2{
	z-index:1;
	position: relative;
}
.container{
	width: 1000px;
	padding: 0;
	margin-top: 5%
}

}
</style>
<body>
	<div class="container">
		<div id="bild">
			<!-- Startbild einfügen -->
			<img id="bild1" src=https://i.imgur.com/1fy9lTO.jpg>
			<img id="bild2" src=https://i.imgur.com/1fy9lTO.jpg>
			<p id="pfeil1" class="Pfeil" onclick="change(-1)"><span class="glyphicon glyphicon-menu-up"></span></p>
			<p id="pfeil2" class="Pfeil" onclick="change(1)"><span class="glyphicon glyphicon-menu-up"></span></p>
			<p id="pfeil3" class="Pfeil" onclick="change(-1)"><span class="glyphicon glyphicon-menu-up"></span></p>
			<p id="pfeil4" class="Pfeil" onclick="change(1)"><span class="glyphicon glyphicon-menu-up"></span></p>
		</div>
		<br>
		Projektarbeit von Carlo/Mathias 2022
		<br>
		<!-- Navigationsleiste mit Buttons (Bootstrap Buttons -> Veränderung der Farbe über die Klasse, welche Klasse welche Farbe bedeutet 
			 ist hier zu finden: https://www.w3schools.com/bootstrap/bootstrap_buttons.asp -->
		<div class="btn-group btn-group-justified">
			<!-- 1 zurück -->
		  <a class="btn btn-info" onmousedown="Funktion(50, 1)"><span class="glyphicon glyphicon-step-backward"></span></a>
			<!-- speed rückwärts -->
		  <a class="btn btn-info" onmousedown="Intervall(10, 5)"><span class="glyphicon glyphicon-backward"></span></a>
			<!-- slow rückwärts -->
		  <a class="btn btn-info" onmousedown="Intervall(25, 5)"><span class="glyphicon glyphicon-chevron-left"></span></a>
			<!-- play -->
		  <a class="btn btn-info" onmousedown="Intervall(25, -5)"><span class="glyphicon glyphicon-play"></span></a>
			<!-- pause: Intervall wird gestoppt -->
		  <a class="btn btn-info" onmousedown="clearInterval(myVar)"><span class="glyphicon glyphicon-pause"></span></a>
			<!-- zum start: Intervall wird gestotppt und Bilder auf Startposition gesetzt -->
		  <a class="btn btn-info" onmousedown="clearInterval(myVar); start()"><span class="glyphicon glyphicon-stop"></span></a>
			<!-- slow vorwärts -->
		  <a class="btn btn-info" onmousedown="Intervall(25, -5)"><span class="glyphicon glyphicon-chevron-right"></span></a>
			<!--speed vorwärts -->
		  <a class="btn btn-info" onmousedown="Intervall(10, -5)"><span class="glyphicon glyphicon-forward"></span></a>
			<!-- 1 vor -->
		  <a class="btn btn-info" onmousedown="Funktion(-50, 1)"><span class="glyphicon glyphicon-step-forward"></span></a>
		</div>
	</div>
	<div id="demo"></div>
</body>
<script type="text/javascript">
/*Breite des Bildes in px */
var b = 2000
/* Breite des Ausschnittes/des Containers #bild*/
var width = 1000

/*Startposition Bild 1*/
var rechts = 0
/*Startposition Bild 2*/
var links = -(2*b)-5

// Startposition der Pfeile
var pfeil1 = 800
var pfeil2 = 1825

var p1
var p2
var p3 = pfeil1 - b
var p4 = pfeil2 - b

/* Variable in der das Intervall zum Aufrufen der Funktion "Funktion" gespeichert wird */
var myVar
/*Variable, die die Schrittweite von der Funktion Intervall auf die Funktion "Funktion" überträgt*/
var minus

/*Startbild*/
var bild = 3

/*Bilder zurück an Startposition*/
function start(){
	rechts = 0
	links = -(2*b)-5
	p1 = pfeil1
	p2 = pfeil2
	p3 = pfeil1 - b
	p4 = pfeil2 - b
	document.getElementById("bild1").style.left = rechts + "px"
	document.getElementById("bild2").style.left = links + "px"
	document.getElementById("pfeil1").style.left = p1+ "px"
	document.getElementById("pfeil2").style.left = p2 + "px"
	document.getElementById("pfeil3").style.left = p3+ "px"
	document.getElementById("pfeil4").style.left = p4 + "px"
	
		p1 = pfeil1
		p2 = pfeil2
		p3 = pfeil1 - b
		p4 = pfeil2 - b 
		
		if (p1 > width+125 || p1 < 175 || bild == 2){
			document.getElementById("pfeil1").style.display = "none"
		} else {
			document.getElementById("pfeil1").style.display = "block"
		}
		if (p2 > width+125 || p2 < 175 || bild == 7){
			document.getElementById("pfeil2").style.display = "none"
		} else {
			document.getElementById("pfeil2").style.display = "block"
		}
		if (p3 > width+125 || p3 < 175 || bild == 2){
			document.getElementById("pfeil3").style.display = "none"
		} else {
			document.getElementById("pfeil3").style.display = "block"
		}
		if (p4 > width+125 || p4 < 175 || bild == 7){
			document.getElementById("pfeil4").style.display = "none"
		} else {
			document.getElementById("pfeil4").style.display = "block"
		}
}

/* Definition und start eines Intervalls; time: pause zwischen Schritten; plus: Schrittweite in px*/
function Intervall(time, plus){
	minus = plus
	/*bereits existierende Intervalle werden gestoppt */
	clearInterval(myVar)
	/*neues Intervall wird definiert und gestartet*/
	myVar = setInterval(Funktion, time)
}

/*Veränderung der Bildposition; plus: Schrittweite*/
function Funktion(plus){
		if (!plus){
			plus = minus
		}
		/*Berechnung der neuen Position der Bilder*/
		rechts += plus 
		links +=plus
		
		/*Anpassen der Bildposition, wenn ein Bild "am Rand angekommen" ist*/
		if (rechts == 0){
			links = -(2*b)-5
		} else if (rechts == -(b-width)){
			links = -(b-width)-5
		} else if (links == -b-5){
			rechts = -b
		} else if (links == -(2*b-width)-5){
			rechts = width
		}
		
		/*Berechnung der neuen Pfeilposition*/
		p1 = rechts + pfeil1
		p2 = rechts + pfeil2
		p3 = links + pfeil1 + b
		p4 = links + pfeil2 + b
		
		/*wenn ein Pfeil sich außerhalb des sichtbaren Bildausschnittes befindet, wird er unsichtbar*/
		if (p1 > width+125 || p1 < 175 || bild == 2){
			document.getElementById("pfeil1").style.display = "none"
		} else {
			document.getElementById("pfeil1").style.display = "block"
		}
		if (p2 > width+125 || p2 < 175 || bild == 7){
			document.getElementById("pfeil2").style.display = "none"
		} else {
			document.getElementById("pfeil2").style.display = "block"
		}
		if (p3 > width+125 || p3 < 175 || bild == 2){
			document.getElementById("pfeil3").style.display = "none"
		} else {
			document.getElementById("pfeil3").style.display = "block"
		}
		if (p4 > width+125 || p4 < 175 || bild == 7){
			document.getElementById("pfeil4").style.display = "none"
		} else {
			document.getElementById("pfeil4").style.display = "block"
		}
		
		
		console.log(rechts, links, p1, p2, p3, p4) /*in der Console wird die aktuelle Bild-/Pfeilposition angezeigt*/
		
		/*im CSS Code wird die neue position übernommen*/
		document.getElementById("bild1").style.left = rechts + "px"
		document.getElementById("bild2").style.left = links + "px"
		document.getElementById("pfeil1").style.left = p1 + "px"
		document.getElementById("pfeil2").style.left = p2 + "px"
		document.getElementById("pfeil3").style.left = p3 + "px"
		document.getElementById("pfeil4").style.left = p4 + "px"
} 

/*Ändern des Bildes und Anpassen der Pfeilposition*/
function change(plus){
	bild += plus
	document.getElementById("bild1").src = bild + ".jpg"
	document.getElementById("bild2").src = bild + ".jpg"
	if (bild == 2){
		pfeil2 =  1140
		document.getElementById("pfeil1").style.display ="none"
		document.getElementById("pfeil3").style.display ="none"
	}
	if (bild == 3){
		pfeil1 = 800
		pfeil2 = 1825
	}
	if (bild == 4){
		pfeil1 = 1650
		pfeil2 = 650
	}
	if (bild == 5){
		pfeil1 = 1120
		pfeil2 = 580
	}
	if (bild == 6){
		pfeil1 = 1740
		pfeil2 = 750
	}
	if (bild == 7){
		pfeil1 = 1780
		document.getElementById("pfeil2").style.display ="none"
		document.getElementById("pfeil4").style.display ="none"
	}
	start()
}

start()
</script>
</html>
