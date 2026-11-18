<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>SAGE - AI Study Mate</title>



<style>

\*{box-sizing:border-box}

body{

&#x20;margin:0;

&#x20;font-family:Arial,sans-serif;

&#x20;background:#f5f3ff;

&#x20;color:#25233b;

}

header{

&#x20;background:#7259d9;

&#x20;color:white;

&#x20;padding:22px;

&#x20;text-align:center;

}

nav{

&#x20;display:flex;

&#x20;justify-content:center;

&#x20;gap:12px;

&#x20;padding:18px;

&#x20;flex-wrap:wrap;

}

button{

&#x20;padding:12px 20px;

&#x20;border:0;

&#x20;border-radius:8px;

&#x20;background:#7259d9;

&#x20;color:white;

&#x20;cursor:pointer;

}

button:hover{background:#503bb0}

.container{

&#x20;max-width:850px;

&#x20;margin:25px auto;

&#x20;padding:20px;

}

.card{

&#x20;background:white;

&#x20;padding:25px;

&#x20;border-radius:14px;

&#x20;margin-bottom:20px;

&#x20;box-shadow:0 3px 12px #00000010;

}

input,textarea{

&#x20;width:100%;

&#x20;padding:13px;

&#x20;border:1px solid #ccc;

&#x20;border-radius:8px;

&#x20;margin:10px 0;

&#x20;font-size:15px;

}

textarea{min-height:180px}

.output{

&#x20;background:#f0edff;

&#x20;padding:18px;

&#x20;border-radius:10px;

&#x20;margin-top:15px;

&#x20;line-height:1.7;

&#x20;white-space:pre-wrap;

}

.hidden{display:none}

h2{color:#7259d9}

footer{

&#x20;text-align:center;

&#x20;padding:25px;

&#x20;color:#777;

}

</style>

</head>



<body>



<header>

<h1>✦ SAGE: AI STUDY MATE</h1>

<p>An AI-Powered Learning Assistant</p>

</header>



<nav>

<button onclick="showPage('home')">Home</button>

<button onclick="showPage('tutor')">Study Tutor</button>

<button onclick="showPage('summary')">Summarize Notes</button>

</nav>



<div class="container">



<section id="home">

<div class="card">

<h2>Welcome to SAGE!</h2>

<p>Your personal study companion.</p>

<p>Learn difficult topics through simple explanations

and convert lengthy notes into concise summaries.</p>

<button onclick="showPage('tutor')">Start Studying</button>

<button onclick="showPage('summary')">Summarize Notes</button>

</div>

</section>



<section id="tutor" class="hidden">

<div class="card">

<h2>AI Study Tutor</h2>

<p>Enter a topic or question.</p>



<input id="topic" placeholder="Enter your topic">



<button onclick="explainTopic()">Explain Topic</button>



<div id="tutorOutput" class="output">

Your explanation will appear here.

</div>

</div>

</section>



<section id="summary" class="hidden">

<div class="card">

<h2>Notes Summarizer</h2>

<p>Paste your study material below.</p>



<textarea id="notes"

placeholder="Paste your notes here..."></textarea>



<button onclick="summarizeNotes()">Summarize</button>



<div id="summaryOutput" class="output">

Your summary will appear here.

</div>

</div>

</section>



</div>



<footer>

<p>SAGE AI STUDY MATE | SEC PROJECT</p>

<p>Review AI-generated content with trusted study materials.</p>

</footer>



<script>



function showPage(page){

&#x20;document.getElementById("home").classList.add("hidden");

&#x20;document.getElementById("tutor").classList.add("hidden");

&#x20;document.getElementById("summary").classList.add("hidden");



&#x20;document.getElementById(page).classList.remove("hidden");

}



function explainTopic(){



&#x20;let topic=document.getElementById("topic").value.trim();



&#x20;if(topic===""){

&#x20; alert("Please enter a topic");

&#x20; return;

&#x20;}



&#x20;document.getElementById("tutorOutput").innerHTML=

&#x20;`<h3>${escapeHTML(topic)}</h3>

&#x20;<b>1. Introduction</b>

&#x20;<p>${escapeHTML(topic)} is the topic you want to understand.

&#x20;Start by learning its definition, purpose and important concepts.</p>



&#x20;<b>2. Step-by-step learning</b>

&#x20;<ol>

&#x20;<li>Understand the basic definition.</li>

&#x20;<li>Identify the main concepts.</li>

&#x20;<li>Study a simple example.</li>

&#x20;<li>Learn its real-world applications.</li>

&#x20;<li>Revise the important points.</li>

&#x20;</ol>



&#x20;<b>3. Simple Analogy</b>

&#x20;<p>Think of learning this topic like understanding a machine:

&#x20;first learn its purpose, then its parts, and finally how they work together.</p>



&#x20;<b>4. Check Your Understanding</b>

&#x20;<p>Can you explain ${escapeHTML(topic)} in your own words

&#x20;and give one example?</p>`;

}



function summarizeNotes(){



&#x20;let text=document.getElementById("notes").value.trim();



&#x20;if(text.length<40){

&#x20; alert("Please enter more study material");

&#x20; return;

&#x20;}



&#x20;let sentences=text.match(/\[^.!?]+\[.!?]+|\[^.!?]+$/g)||\[];



&#x20;let words=text.toLowerCase().match(/\[a-z]{4,}/g)||\[];



&#x20;let frequency={};



&#x20;let stop=\["this","that","with","from","have","were",

&#x20;"they","them","their","there","then","into","about",

&#x20;"which","while","when","what","your","you","are",

&#x20;"for","the","and","but","not","can","will","was"];



&#x20;words.forEach(word=>{

&#x20; if(!stop.includes(word)){

&#x20;  frequency\[word]=(frequency\[word]||0)+1;

&#x20; }

&#x20;});



&#x20;let important=Object.keys(frequency)

&#x20;.sort((a,b)=>frequency\[b]-frequency\[a])

&#x20;.slice(0,8);



&#x20;let scored=sentences.map((sentence,index)=>{

&#x20; let count=0;

&#x20; sentence.toLowerCase().split(/\\W+/).forEach(word=>{

&#x20;  count+=frequency\[word]||0;

&#x20; });

&#x20; return {sentence,index,score:count};

&#x20;});



&#x20;let selected=scored

&#x20;.sort((a,b)=>b.score-a.score)

&#x20;.slice(0,Math.max(2,Math.ceil(sentences.length\*.25)))

&#x20;.sort((a,b)=>a.index-b.index);



&#x20;let summary=selected.map(x=>x.sentence).join(" ");



&#x20;let questions=important.slice(0,3).map(word=>

&#x20; "What does "+word+" mean in these notes?"

&#x20;);



&#x20;document.getElementById("summaryOutput").innerHTML=

&#x20;`<h3>TL;DR Summary</h3>

&#x20;<p>${escapeHTML(summary)}</p>



&#x20;<h3>Important Key Terms</h3>

&#x20;<ul>${important.map(w=>"<li>"+escapeHTML(w)+"</li>").join("")}</ul>



&#x20;<h3>Self-Check Questions</h3>

&#x20;<ol>${questions.map(q=>"<li>"+escapeHTML(q)+"</li>").join("")}</ol>`;

}



function escapeHTML(value){

&#x20;return value.replace(/\[\&<>"']/g, char => ({

&#x20; '\&':'\&amp;',

&#x20; '<':'\&lt;',

&#x20; '>':'\&gt;',

&#x20; '"':'\&quot;',

&#x20; "'":'\&#39;'

&#x20;}\[char]));

}



</script>



</body>

</html>

