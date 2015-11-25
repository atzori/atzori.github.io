---
title: GH Fun
layout: simple_page
---


# GH Workaround

Drag an drop the following link (a *flipr*) to your browser's bookmarks bar: <a href="javascript:
var l=window.location.href;if(l.indexOf('https://github.com/')>=0){l=l.slice(19);window.location.href='http://gh.cagliarifornia.org/'+l;} else {window.location.href='http://gh.cagliarifornia.org/no';};">GH Workaround</a>. 
Then, whenever you are on a GH page, just click on the link on the bookmarks bar 
and the browser will jump to the its corresponding page.


To simplify the use of SWiPE, drag an drop the following link (a *flipr*) to your browser's bookmarks bar: <a href="javascript:
var l=window.location.href;if(l.indexOf('.wikipedia.org/wiki/')>0){l=l.split('/');l=l[l.length-1];window.location.href='http://swipe.webofcode.org/wiki/'+l;} else if(l.indexOf('.webofcode.org/wiki/')>0){l=l.split('/');l=l[l.length-1];window.location.href='http://en.wikipedia.org/wiki/'+l;}else{window.location.href='http://swipe.webofcode.org/';};">SwipeFlip</a>. Then, whenever you are on a Wikipedia page, just click on the new SWiPE link on the bookmarks bar and the browser will jump to the its corresponding SWiPE page.






```
var l=window.location.href;
if(l.indexOf('.wikipedia.org/wiki/')>0){
	l=l.split('/');l=l[l.length-1];window.location.href='http://swipe.webofcode.org/wiki/'+l;
} else if(l.indexOf('.webofcode.org/wiki/')>0){
	l=l.split('/');l=l[l.length-1];window.location.href='http://en.wikipedia.org/wiki/'+l;
	}else{
		window.location.href='http://gh.cagliarifornia.org/no';
};



var l=window.location.href;if(l.indexOf('https://github.com/')>=0){l=l.slice(19);window.location.href='http://gh.cagliarifornia.org/'+l;} else {window.location.href='http://gh.cagliarifornia.org/no';};