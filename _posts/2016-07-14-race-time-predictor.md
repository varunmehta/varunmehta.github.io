---
title: "Race Time Predictor"
layout: post
date: 2016-07-14
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- running
star: false
hidden: false
category: blog
author: varunmehta
description: Race Time Predictor
---
<script type="text/javascript" language="javascript">
function predictRacePace() {
    var d1 = document.getElementById('d1').value;
    var t1 = document.getElementById('t1').value;
    var d2 = document.getElementById('d2').value;

    t1 = convertHMS2S(t1);

    var t2 = predictPace(d1, t1, d2);

    t2P = time2Pace(t2, d2);

    t2 = convertStoHMS(t2);
    document.getElementById('t2').value = t2;
    document.getElementById('t2P').value = t2P;
}

function time2Pace(t2, d2) {
    pace = t2 / d2;
    return convertStoHMS(pace);
}


/*
  Pure math function for calculation

  T1 is the time achieved for D1 in seconds
  T2 is the time predicted for D2 in seconds
  D1 is the distance over which the initial time is achieved. (any unit)
  D2 is the distance for which the time is to be predicted. (same as D1 units)
*/
function predictPace(d1, t1, d2) {
    var d = Math.pow((d2 / d1), 1.06);
    return t1 * d;
}

/*
  This function handels "HH:MM:SS" as well as "MM:SS" or "SS", and converts it to seconds.
*/
function convertHMS2S(hms) {
    var p = hms.split(':'),
        s = 0,
        m = 1;

    while (p.length > 0) {
        s += m * parseInt(p.pop(), 10);
        m *= 60;
    }

    return s;
}

/**
  This method will convert a given amount of seconds to HH:mm:ss format
*/
function convertStoHMS(s) {
    var secs = s % 60;
    s = (s - secs) / 60;
    secs = Math.floor(secs);
    var mins = s % 60;
    var hrs = (s - mins) / 60;

    return (hrs > 0 ? hrs + ':' : '') + (mins < 10 ? ('0' + mins) : mins) + ':' + (secs < 10 ? ('0' + secs) : secs);
}

</script>

<div dir="ltr" style="text-align: left;" trbidi="on">

This race time predictor is based off Peter Reigel's formula for race pace prediction.<br />
<a href="https://en.wikipedia.org/wiki/Peter_Riegel#Race_time_prediction">https://en.wikipedia.org/wiki/Peter_Riegel#Race_time_prediction</a><br />
<br />
T2 = T1 × (D2÷D1) ^ 1.06<br />
<br />
<ul style="text-align: left;">
<li>T1 is the time achieved for D1</li>
<li>T2 is the time predicted for D2</li>
<li>D1 is the distance over which the initial time is achieved.</li>
<li>D2 is the distance for which the time is to be predicted.</li>
</ul>
<br />
<b>Example</b><br />
T1 = 9:28 minutes<br />
D1 = 1 miles<br />
D2 = 13.1 miles<br />
<div>
T2 ~= 2:24:00 (HH:mm:ss)</div>
<div>
<br />
<h2 style="text-align: left;">Calculator</h2>
I just whipped a quick one up in javascript, there are bunch of them available on the internet, but wanted to write one for my blog :)<br />
<br />

<table>
<tr><td>Distance Run:</td><td> <input id="d1" type="text" /> </td></tr>
<tr><td>Time Taken to Run above distance (HH:mm:ss):</td><td>  <input id="t1" type="text" /> </td></tr>
<tr><td>Next Planned Race distance:</td><td> <input id="d2" type="text" /> </td></tr>
<tr><td colspan="2"><input onclick="predictRacePace()" type="button" value="Calculate Pace" /> </td></tr>

<tr><td colspan="2">
<h2>Results</h2>
</tr></td>

<tr><td>Predicted time to finish race:</td><td> <input id="t2" type="text" /> </td></tr>
<tr><td>Predicted pace to finish race:</td><td> <input id="t2P" type="text" /></td></tr>
</table>
<br />
<hr />
<h1></h1>
Jack Daniel's Calculator.
<iframe src="http://runsmartproject.com/calculator/embed/index.php?title=false" width="600" height="1000" frameborder="0"></iframe>
</div>
</div>
