# Persistent-Form-Fields
Tamptermonkey/Greasemonkey script to make form-field-values persistent.
It stays the way, last time you left it.

# Prerequisites
* For chrome: [Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)
* For firefox: [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/)

# Usage
[How to manually install a Greasemonkey script ](https://www.fimfiction.net/blog/56868/how-to-manually-install-a-greasemonkey-script)

# Script

```
// ==UserScript==
// @name         Persistent Form Fields
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==

function BindLocalStorage(){
            console.log("Setting up local storage...");

             /*
             * when a form field changes store it's value in local storage
             */            

            var inputTag = document.getElementsByTagName('input');
            for (var i = inputTag.length - 1; i >= 0; i--) {
                var id = inputTag[i].getAttribute("id");
                //console.log(id);                
                //console.log(value);
                if (typeof(Storage) !== "undefined") {
                    var value = localStorage.getItem(id);
                    inputTag[i].value = value;
                }

                inputTag[i].oninput = function() { 
                    var id = this.getAttribute("id");                    
                    //console.log(id);
                    localStorage.setItem(id,this.value);
                    var value = localStorage.getItem(id);
                    //console.log("Local: "+value);
                };
            } 
};

(function() {
    'use strict';
    BindLocalStorage();
    $(document).ready(function () {            
            BindLocalStorage();
        });        
})();
```
