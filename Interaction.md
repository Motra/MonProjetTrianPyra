# MonProjetTrianPyra
/*
 * variables globales
 */
var canvas = document.getElementById("myCanvas");
var graphicContext = canvas.getContext("2d");
 
 
/**
 * dessine un rectangle 
 * @param {Number} x abscisse du coin supérieur gauche du rectangle
 * @param {Number} y ordonnée du coin supérieur gauche du rectangle
 * @param {Number} L longueur du rectangle
 * @param {Number} H hauteur du rectangle
 * @param {String} couleurTrait la couleur du contour du rectangle
 * @param {String} couleurRemplissage la couleur de remplissage du rectangle
 */
function rectangle(x, y, L, H, couleurTrait, couleurRemplissage) {
    graphicContext.lineWidth = 3;
    graphicContext.strokeStyle = couleurTrait;
    graphicContext.fillStyle = couleurRemplissage;
    graphicContext.fillRect(x, y, L, H);
    graphicContext.strokeRect(x, y, L, H);
}

/**
 * dessine un escalier droit
 * @param {Number} nbMarches nombre de marches
 * @param {Number} hauteur d'une marche (en pixels)
 * @param {String} couleurTrait la couleur du contour du rectangle
 * @param {String} couleurRemplissage la couleur de remplissage du rectangle
 */
function dessinerEscalier(nbMarches, hauteur, couleurTrait, couleurRemplissage) {
    var x = 0;
    var y = 0;
    var largeur = hauteur;
    for (var i = 1; i <= nbMarches; i++) {
        rectangle(x, y, largeur, hauteur, couleurTrait, couleurRemplissage);
        y = y + hauteur;
        largeur = largeur + hauteur;
    }
}

/**
 * dessine un escalier pyramidal
 * @param {Number} nbMarches nombre de marches
 * @param {Number} hauteur d'une marche (en pixels)
 * @param {String} couleurTrait la couleur du contour d'une marche
 * @param {String} couleurRemplissage la couleur de remplissage d'une marche
 */
function dessinerPyramide(nbMarches, hauteur, couleurTrait, couleurRemplissage) {
    var x = canvas.width / 2 - hauteur;
    var y = 0;
    var largeur = 2* hauteur;
    for (var i = 1; i <= nbMarches; i++) {
        rectangle(x, y, largeur, hauteur, couleurTrait, couleurRemplissage);
        y = y + hauteur;
        x = x - hauteur;
        largeur = largeur + 2* hauteur;
    }
}
 
/**
 * efface le canvas
 */
function effacer() {
    graphicContext.clearRect(0, 0, canvas.width, canvas.height);
}
 
/**
 * fonction appelée au chargement de la page
 * (attribut onload de la balise body, cet événement a lieu une fois que 
 * la page est chargée et le DOM entièrement créé).
 */
function init() {
 
  // associe une fonction de gestion à l'événement onclick du bouton 'dessiner'
    document.getElementById("dessiner").onclick = function () {
        var nb = parseInt(document.getElementById("nbreMarches").value);
        var hauteur = parseInt(document.getElementById("hauteurMarche").value);
        var strokeColor = document.getElementById("strokeColor").value;
        var fillColor = document.getElementById("fillColor").value;
        var escalier = document.getElementById("escalier").checked;
        if (escalier) {
           dessinerEscalier(nb, hauteur, strokeColor, fillColor);
        } else {
           dessinerPyramide(nb, hauteur, strokeColor, fillColor); 
        }
    };
    
     // associe une fonction de gestion à l'événement onclick du bouton 'effacer'
    document.getElementById("effacer").onclick = function () {
        effacer();
    };
}
