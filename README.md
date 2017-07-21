<h2><code>RedAlert</code>/<code>"צבע-אדום"</code> API</h2>

<h1><em>CURRENTLY UNAVAILABLE!</em></h1>

<em>The archive is password protected, and no-one will ever get the password. Below there is some legacy description.</em>

<hr/>

<blockquote>
Red-Alert (<code>צבע אדום</code>) is a the name called for the missile-alarm,
hitting the country of Israel from surrounding hostile "neighbors".

While- there is <strong>no official</strong> way of accessing any
of the "where is there an alarm right now?" information, "as an external API"..
..The information itself is quite easy to reverse-engineer from the <a href="http://www.oref.org.il">oref.org.il</a>-website's structure and external JSON/JavaScript resources.

<h3><em>Will No Be Explained In-Here!</em></h3>
</blockquote>

<hr/>

Warning: do not relay on this service at time of emergencies and always be attentive for reports TV/Radio, Sirens, etc...

How this works?
I'm providing a proxy,
to a <code>data-json</code> from <strong>Pikud Ha' Oref</strong>.

Why?
<ol>
  <li>
  adding very permissive CORS-headers so the information can be retrieved by a browser's client-side (including all HTTP-headers!).
  </li>
  <li>
  providing charset fix, to either UTF-8, or ASCII-escaped variation ("\u....").
  </li>
  <li>
  also available <code>JSONP</code> as an alternative to fetching with xhr.
  debug mode and other "stuff"...
  </li>
</ol>

<table>
<thead><tr><td>switch</td><td>meanings (EN)</td><td>meanings (HE)</td></tr></thead>
<tbody>
  <tr><td><code>beautify</code></td><td>format the JSON for easier readability.</td><td>פורס את המידע על פני כמה שורות באופן שקל יותר לצפות בו</td></tr>
  <tr><td><code>callback</code></td><td>wrap the data in <code>window.alersLog(...data...);</code> so it can be used for <a href="http://en.wikipedia.org/wiki/JSONP" title="JSON Protocol">JSON-P</a>, there is no changing of the callback method-name.</td><td>עוטף את המידע בפונקציה שתופעל בעת הקריאה, שם הפונקציה לא ניתן לשינוי</td></tr>
</tbody>
</table>

Example 1: Plain JavaScript-callback ("JSON-P")

```js
window.alertsLog = function(jsonData){
  console.log(jsonData);
};
```

Example 2: Dynamic and repeating JavaScript-callback ("JSON-P").

<em>Essentially repentingly <code>&lt;script&gt;</code> injection into the DOM, in-order to deliver the new information.</em>

```js
(function(s,u){
  // add something random, prevent browser caching the result.
  u += (u.indexOf("?") === -1 ? "?" : "&") + "__=" + (1*new Date());  //like so.
 
  s.setAttribute("src", u);
  document.getElementsByTagName("body")[0].appendChild(s);
}(
document.createElement("script"),
"http://redalert.eladkarako.com/alerts_json.php?callback"
));
 
/* skip async and type="text/javascript", its redundant. */
```

<br/>

<table>
<thead><tr><td>switch</td><td>meanings (EN)</td><td>meanings (HE)</td></tr></thead>
<tbody>
  <tr><td><code>nounicode</code></td><td>The Hebrew letter ALEF (<code>א</code>) is <code>\u05D0</code>. Use this switch to deliver the content in a not-ASCII safe mode, but a plain UTF-8.</td><td>עבור שימוש או צפייה בתוכן ללא קידוד יוניקוד</td></tr>
  <tr><td><code>debug</code></td><td>Will show an alternative output (also <code>JSON</code> formatted), that will include the <code>script used data</code>, <code>request headers</code>, <code>response headers</code>, and an additional <code>extended response-information</code>, to avoid processing a large amount of data, and keep your application fast, avoid using this switch in <code>production</code> only use it manually in <code>debug mode</code></td><td>עבור מצב דיבאג, מפרט את התקשורת היוצאת וחוזרת לרבות מידע לגבי השרתים ומידע טכני רב, יש להמנע משימוש, למעט בדיקות תקינות וכדומה</td></tr>
</tbody>
</table>


More information is available <a href="http://icompile.eladkarako.com/%D7%A6%D7%91%D7%A2-%D7%90%D7%93%D7%95%D7%9D-api/" title="http://icompile.eladkarako.com/צבע-אדום-api/">on the original-article</a>,
covering the usage of the API in various other ways.

<hr/>

<sub>This API is given free of charge!<br/>You shall not charge anyone for using this API, you shall not use this API with any ads-showing or statistics collecting products,<br/>this includes <strong>any</strong> useage analytics services! <strong>yes. Google Analytics too!</strong><br/>The API service is keeping the identity (IP and other unique-identifications). Abusing the API/Service - <strong>will get you be blocked and reported</strong>.</sub>
