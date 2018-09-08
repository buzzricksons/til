```
/* 
 * S5 Custom CSS
 * author:luke, a-kato
 */ 
/*--------------------For本文--------------------*/ 
.wiki-content h1, 
.wiki-content h2, 
.wiki-content h3, 
.wiki-content h4, 
.wiki-content h5, 
.wiki-content h6 { 
 margin: 1.3em 0 1em; 
 padding: 0; 
 font-weight: bold; 
} 
.wiki-content h1 { 
 font-size: 1.9em; 
 border-bottom: 3px solid #ddd; 
} 
.wiki-content h2 { 
 padding:0 0 0 10px !important;
 border-left:#a3a3a3 8px solid;
 background: #efefef;
 font-weight: bold;
 color:#000 !important;
 font-size: 1.6em;
} 
.wiki-content h3 { 
 text-align:left; 
 margin:1em 0px; 
 padding:0 5px 0 10px; 
 border-width:0px 0px 0px 5px; 
 border-left-style:solid; 
 border-left-color:#336699; 
 font-size: 1.3em; 
 height: 1.2em;
 line-height: 1.3;
} 
.wiki-content h4 { 
 font-size: 1.2em; 
 margin-left:-2px; 
} 
.wiki-content h4:before{ 
 content: "■"; 
 position: relative; 
 padding-right:7px; 
 top: -2px;
/*---- font-size: .6rem;----------*/
} 
.wiki-content h5 { 
 font-size: 1.1em; 
} 
.wiki-content h6 { 
 font-size: 1em; 
}
.wiki-content pre code { 
 font-size: 1.2em;
 background-color:#cccccc; 
}
.wiki-content code:not([class]) {
 margin: 0 0.15em;
 padding: 0 0.3em;
 white-space: pre-wrap;
 border: 3px solid #e2e2e2;
 background-color: #e2e2e2;
 border-radius: 3px;
 line-height: 2;
 display: inline; /* added to fix Yahoo block display of inline code */
}
/*--------------------/For本文--------------------*/ 
/*--------------------For目次--------------------*/ 
.client-side-toc-macro:before { 
 content:"目次"; 
 color:#5e5e5e; 
} 
.client-side-toc-macro { 
 background-color:#cccccc; 
 padding:10px; 
 border:1px solid #8c8c8c; 
}
.client-side-toc-macro a {
 color: #3572b0;
}
.client-side-toc-macro a:link {
 text-decoration: none;
}
.client-side-toc-macro a:hover {
 text-decoration: underline;
} 
.client-side-toc-macro li{
 list-style: none;
}
/*--------------------/For目次--------------------*/
/*--------------------無地テンプレートを使わせない仕組み--------------------*/ 
#quick-create-page-button {
  display: none;
}
#create-page-button {
  border-radius: 2px; 
}
/*--------------------/無地テンプレートを使わせない仕組み--------------------*/
```