# MarkDown Here
Mark Down CSS設定(for DARK theme)

## スタイリングCSS
```
/*
 * NOTE:
 * - The use of browser-specific styles (-moz-, -webkit-) should be avoided.
 * If used, they may not render correctly for people reading the email in
 * a different browser than the one from which the email was sent.
 * - The use of state-dependent styles (like a:hover) don't work because they
 * don't match at the time the styles are made explicit. (In email, styles
 * must be explicitly applied to all elements -- stylesheets get stripped.)
 */

/* This is the overall wrapper, it should be treated as the `body` section. */
.markdown-here-wrapper {
}

/* To add site specific rules, you can use the `data-md-url` attribute that we
  add to the wrapper element. Note that rules like this are used depending
  on the URL you're *sending* from, not the URL where the recipient views it.
*/
/* .markdown-here-wrapper[data-md-url*="mail.yahoo."] ul { color: red; } */

pre, code {
  font-size: 1em;
  font-family: Consolas, Inconsolata, Courier, monospace;
}

code {
  margin: 0 0.15em;
  padding: 0 0.3em;
  white-space: pre-wrap;
  border: 2px solid #EAEAEA;
  background-color: #e2e2e2;
  border-radius: 3px;
  display: inline; /* added to fix Yahoo block display of inline code */
}

pre {
  font-size: 1em;
  line-height: 1.2em;
}

pre code {
  white-space: pre;
  overflow: auto; /* fixes issue #70: Firefox/Thunderbird: Code blocks with horizontal scroll would have bad background colour */
  border-radius: 3px;
  border: 1px solid #666;
  padding: 0.5em 0.7em;
  display: block !important; /* added to counteract the Yahoo-specific `code` rule; without this, code blocks in Blogger are broken */
}

/* In edit mode, Wordpress uses a `* { font: ...;} rule+style that makes highlighted
code look non-monospace. This rule will override it. */
.markdown-here-wrapper[data-md-url*="wordpress."] code span {
  font: inherit;
}

/* Wordpress adds a grey background to `pre` elements that doesn't go well with
our syntax highlighting. */
.markdown-here-wrapper[data-md-url*="wordpress."] pre {
  background-color: transparent;
}

/* This spacing has been tweaked to closely match Gmail+Chrome "paragraph" (two line breaks) spacing.
Note that we only use a top margin and not a bottom margin -- this prevents the
"blank line" look at the top of the email (issue #243).
*/
p {
  /* !important is needed here because Hotmail/Outlook.com uses !important to
  kill the margin in <p>. We need this to win. */
  margin: 0 0 1.2em 0 !important;
}

table, pre, dl, blockquote, q, ul, ol {
  margin: 1.2em 0;
}

ul, ol {
  padding-left: 2em;
}

li {
  margin: 0.5em 0;
}

/* Space paragraphs in a list the same as the list itself. */
li p {
  /* Needs !important to override rule above. */
  margin: 0.5em 0 !important;
}

/* Smaller spacing for sub-lists */
ul ul, ul ol, ol ul, ol ol {
  margin: 0;
  padding-left: 1em;
}

/* Use Roman numerals for sub-ordered-lists. (Like Github.) */
ol ol, ul ol {
  list-style-type: lower-roman;
}

/* Use letters for sub-sub-ordered lists. (Like Github.) */
ul ul ol, ul ol ol, ol ul ol, ol ol ol {
  list-style-type: lower-alpha;
}

dl {
  padding: 0;
}

dl dt {
  font-size: 1em;
  font-weight: bold;
  font-style: italic;
}

dl dd {
  margin: 0 0 1em;
  padding: 0 1em;
}

blockquote, q {
  border-left: 4px solid #919191;
  padding: 0 1em;
  color: #a6a6a6;
  quotes: none;
}

blockquote::before, blockquote::after, q::before, q::after {
  content: none;
}

h1, h2, h3, h4, h5, h6 {
  margin: 1.3em 0 1em;
  padding: 0;
  font-weight: bold;
}

h1 {
  font-size: 1.8em;
  border-bottom: 2px solid #ddd;
}

h2 {
  text-align:left;
  margin:1em 0px;
  padding:5px 0 5px 10px !important;
  border-width:0px 0px 0px 5px;
  border-left-style:solid;
  border-left-color:rgb(105,147,123);
  background-color: #595959;
  font-size: 1.6em;
  color:rgb(51,51,51);
}

h3 {
  text-align:left;
  margin:1em 0px;
  padding:0 5px 0 10px;
  border-width:0px 0px 0px 5px;
  border-left-style:solid;
  border-left-color:#336699;
  font-size: 1.3em;
  height:1.3em;
  color:rgb(77, 77, 77);
}

h4 {
  font-size: 1.2em;
  margin-left:-2px;
}

h4:before{
  content: "■";
  position: relative;
  top: -2px;
  padding-right:7px;
}

h5 {
  font-size: 1.1em;
}

h6 {
  font-size: 1em;
  color: #777;
}

table {
  padding: 0;
  border-collapse: collapse;
  border-spacing: 0;
  font-size: 1em;
  font: inherit;
  border: 0;
}

tbody {
  margin: 0;
  padding: 0;
  border: 0;
}

table tr {
  border: 0;
  border-top: 1px solid #CCC;
  background-color:rgba(0,0,0,0.3);
  margin: 0;
  padding: 0;
}

table tr:nth-child(2n) {
  background-color: rgba(0,0,0,0.3);
}

table tr th, table tr td {
  font-size: 1em;
  border: 1px solid #CCC;
  margin: 0;
  padding: 0.5em 1em;
}

table tr th {
 font-weight: bold;
  background-color: #777777;
}
```

## シンタックスハイライティングCSS
```
/*
Monokai style - ported by Luigi Maselli - http://grigio.org
*/

.hljs {
  display: block;
  overflow-x: auto;
  padding: 0.5em;
  background: #272822;
  -webkit-text-size-adjust: none;
}

.hljs-tag,
.hljs-tag .hljs-title,
.hljs-keyword,
.hljs-literal,
.hljs-strong,
.hljs-change,
.hljs-winutils,
.hljs-flow,
.nginx .hljs-title,
.tex .hljs-special {
  color: #f92672;
}

.hljs {
  color: #ddd;
}

.hljs .hljs-constant,
.asciidoc .hljs-code {
    color: #66d9ef;
}

.hljs-code,
.hljs-class .hljs-title,
.hljs-header {
    color: white;
}

.hljs-link_label,
.hljs-attribute,
.hljs-symbol,
.hljs-symbol .hljs-string,
.hljs-value,
.hljs-regexp {
    color: #bf79db;
}

.hljs-link_url,
.hljs-tag .hljs-value,
.hljs-string,
.hljs-bullet,
.hljs-subst,
.hljs-title,
.hljs-emphasis,
.hljs-type,
.hljs-preprocessor,
.hljs-pragma,
.ruby .hljs-class .hljs-parent,
.hljs-built_in,
.django .hljs-template_tag,
.django .hljs-variable,
.smalltalk .hljs-class,
.hljs-javadoc,
.django .hljs-filter .hljs-argument,
.smalltalk .hljs-localvars,
.smalltalk .hljs-array,
.hljs-attr_selector,
.hljs-pseudo,
.hljs-addition,
.hljs-stream,
.hljs-envvar,
.apache .hljs-tag,
.apache .hljs-cbracket,
.tex .hljs-command,
.hljs-prompt {
  color: #a6e22e;
}

.hljs-comment,
.hljs-annotation,
.smartquote,
.hljs-blockquote,
.hljs-horizontal_rule,
.hljs-decorator,
.hljs-template_comment,
.hljs-pi,
.hljs-doctype,
.hljs-deletion,
.hljs-shebang,
.apache .hljs-sqbracket,
.tex .hljs-formula {
  color: #75715e;
}

.hljs-keyword,
.hljs-literal,
.css .hljs-id,
.hljs-phpdoc,
.hljs-dartdoc,
.hljs-title,
.hljs-header,
.hljs-type,
.vbscript .hljs-built_in,
.rsl .hljs-built_in,
.smalltalk .hljs-class,
.diff .hljs-header,
.hljs-chunk,
.hljs-winutils,
.bash .hljs-variable,
.apache .hljs-tag,
.tex .hljs-special,
.hljs-request,
.hljs-status {
  font-weight: bold;
}

.coffeescript .javascript,
.javascript .xml,
.tex .hljs-formula,
.xml .javascript,
.xml .vbscript,
.xml .css,
.xml .hljs-cdata {
  opacity: 0.5;
}
```