# Tarea4_CRIPTO

// ==UserScript==
// @name         LAB4_Cripto.tiiny
// @namespace    http://example.com/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        https://lab4.tiiny.site
// @require      https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.2.0/crypto-js.min.js#sha512-a+SUDuwNzXDvz4XrIcXHuCf089/iJAoN4lmrXJg18XnduKK6YlDHNRalv4yd1N40OKI80tFidF+rqTFKGPoWFQ==
// @icon         https://www.google.com/s2/favicons?sz=64&domain=instructure.com
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    let texto1 = "";
    //selecciono el parrafo de la pagina web
    const paragraph = document.querySelector('p');
    //se extrae el texto del parrafo
    let texto = paragraph.innerText;
    // Divide el texto en oraciones utilizando el punto como separador
    let oraciones = texto.split('.');
    let primerosCaracteres = oraciones.map(function(oracion) {
        // Obtiene el primer caracter de cada oracion
        return oracion.trim().charAt(0);
    });
    // Unir los primeros caracteres en un solo string
    let resultado = primerosCaracteres.join('');
    if (resultado.length > 0) {
        console.log('La llave es: ' + resultado);
    } else {
        console.log('No se encontraron oraciones en el texto.');
    }
    function MensajeCifrado(){
        //Donde se obtienen todos los div en la pagina web
        const divElements = document.querySelectorAll("div");
        console.log("Los mensajes cifrados son: "+ divElements.length);
    }
    MensajeCifrado();
    function decipherMessage(des3Key) {
        const divElements = document.querySelectorAll("div");
        divElements.forEach((div) => {
            const id = div.id.toString();
            const descifrado = CryptoJS.TripleDES.decrypt(id, des3Key, {
                mode: CryptoJS.mode.ECB});
            const id_decrypt = descifrado.toString(CryptoJS.enc.Utf8);
            console.log(id +' '+ id_decrypt);
            texto1 = texto1 + id_decrypt + "<br>";
        });
    }
    const concatenatedLetters = resultado;
    const des3Key = CryptoJS.enc.Utf8.parse(concatenatedLetters);
    decipherMessage(des3Key);
    paragraph.insertAdjacentHTML("beforeend", "<br><br>" + texto1);
})();
