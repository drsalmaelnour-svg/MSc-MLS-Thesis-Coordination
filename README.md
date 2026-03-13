<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MSc MLS Thesis Coordination Dashboard</title>

<style>
body{font-family:Arial,Helvetica,sans-serif;margin:0;background:#f4f6fb;color:#1e293b}
header{background:#0f2f4a;color:white;padding:20px}
header h1{margin:0;font-size:22px}
header p{margin:4px 0 0;font-size:14px;opacity:.9}
.container{padding:30px;max-width:1200px;margin:auto}
.card{background:white;border-radius:10px;padding:20px;margin-bottom:25px;box-shadow:0 6px 18px rgba(0,0,0,.08)}
button{padding:10px 14px;border:none;background:#0f2f4a;color:white;border-radius:6px;cursor:pointer}
button:hover{opacity:.9}
table{width:100%;border-collapse:collapse;margin-top:15px}
th,td{padding:10px;border-bottom:1px solid #e5e7eb;text-align:left;font-size:14px}
th{background:#f1f5f9}
.link{color:#2563eb;text-decoration:none}
.portal{max-width:600px;margin:auto;padding:40px}
input,textarea,select{width:100%;padding:10px;margin-top:8px;margin-bottom:14px;border:1px solid #cbd5e1;border-radius:6px}
textarea{height:120px}
.notice{background:#f1f5f9;padding:12px;border-radius:6px;margin-bottom:20px}
</style>
</head>

<body>

<header>
<h1>MSc MLS Thesis Coordination Dashboard</h1>
<p>MSc Medical Laboratory Science Program · College of Health Sciences · Gulf Medical University</p>
</header>

<div class="container" id="dashboard">

<div class="card">
<h2>Upload Student CSV</h2>
<p>Upload a CSV file containing the following columns:</p>
<div class="notice">
Reg No, Student Name, Student Email, Supervisor, Supervisor Email, Co-Supervisor
</div>

<input type="file" id="csvUpload" accept=".csv">
<button onclick="loadCSV()">Import Students</button>
</div>

<div class="card">
<h2>Student Registry</h2>

<table id="studentTable">
<thead>
<tr>
<th>Reg No</th>
<th>Name</th>
<th>Supervisor</th>
<th>Portal</th>
<th>Copy Link</th>
</tr>
</thead>
<tbody></tbody>
</table>
</div>

</div>

<div id="studentPortal" class="portal" style="display:none"></div>

<script>

let students = JSON.parse(localStorage.getItem("students")) || [];

function generateToken(){
return Math.random().toString(36).substring(2,12);
}

function loadCSV(){

const file=document.getElementById("csvUpload").files[0];
const reader=new FileReader();

reader.onload=function(e){

const rows=e.target.result.split("\n").slice(1);

students=rows.map(row=>{

const cols=row.split(",");

const token=generateToken();

return{
regNo:cols[0]?.trim(),
name:cols[1]?.trim(),
email:cols[2]?.trim(),
supervisor:cols[3]?.trim(),
supervisorEmail:cols[4]?.trim(),
cosupervisor:cols[5]?.trim(),

orcid:"",

proposalReflection:"",
progressReflection:"",
defenseReflection:"",

status:"active",


token:token,

link:`${window.location.origin}${window.location.pathname}?student=${cols[0]?.trim()}&token=${token}`

};

});

localStorage.setItem("students",JSON.stringify(students));

renderStudents();

}

reader.readAsText(file);

}

function renderStudents(){

const table=document.querySelector("#studentTable tbody");

if(!table) return;









table.innerHTML="";

students.forEach(s=>{

if(!s.regNo) return;

table.innerHTML+=`

<tr>
<td>${s.regNo}</td>
<td>${s.name}</td>
<td>${s.supervisor}</td>
<td><a class="link" href="${s.link}" target="_blank">Open Portal</a></td>
<td><button onclick="copyLink('${s.link}')">Copy</button></td>
</tr>

`;

});

}

function copyLink(link){
navigator.clipboard.writeText(link);
alert("Student portal link copied");
}

renderStudents();

const params=new URLSearchParams(window.location.search);

const studentID=params.get("student");
const token=params.get("token");

if(studentID && token){
loadStudentPortal(studentID,token);
}

function loadStudentPortal(regNo,token){

const student=students.find(s=>s.regNo===regNo && s.token===token);

if(!student){
document.body.innerHTML="<h2 style='padding:40px'>Invalid or expired link</h2>";
return;
}



document.getElementById("dashboard").style.display="none";

const portal=document.getElementById("studentPortal");

portal.style.display="block";

portal.innerHTML=`

<h2>Hello ${student.name}</h2>

<p><b>Reg No:</b> ${student.regNo}</p>

<h3>Submit ORCID</h3>

<input id="orcid" placeholder="Enter ORCID ID">

<button onclick="submitORCID('${student.regNo}')">Submit ORCID</button>


<h3>Submit Reflection</h3>

<select id="milestone">
<option>Proposal Presentation</option>
<option>Progress Report</option>
<option>Defense Preparation</option>
</select>

<textarea id="reflection" placeholder="Write your reflection"></textarea>

<button onclick="submitReflection('${student.regNo}')">Submit Reflection</button>

`;

}

function submitORCID(regNo){

let students=JSON.parse(localStorage.getItem("students"));

const student=students.find(s=>s.regNo===regNo);

student.orcid=document.getElementById("orcid").value;

localStorage.setItem("students",JSON.stringify(students));

alert("ORCID saved successfully");

}

function submitReflection(regNo){

const milestone=document.getElementById("milestone").value;

const reflection=document.getElementById("reflection").value;

let reflections=JSON.parse(localStorage.getItem("reflections")) || [];

reflections.push({
regNo:regNo,
milestone:milestone,
reflection:reflection,
date:new Date()
});

localStorage.setItem("reflections",JSON.stringify(reflections));

alert("Reflection submitted successfully");

}

</script>

</body>
</html>
