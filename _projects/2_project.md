---
layout: page
title: Office Hours Notification System
description: Enhanced ease of use of TA request system
img: assets/img/oh_notif_screenshot.jpeg
importance: 4
category: fun
---

<em>Author:</em> Inbar Ofer

- Project code can be found [here](https://script.google.com/d/15BPkvuq53yt_keMI4ZD5bAdR3GkYExFAzY59ZhyDcbhwxqbeK6x3PV76/edit?usp=sharing).

## Overview

This is a Google Apps Script that creates a trigger for a Google Sheets file. When students edit the spreadsheet to request help, the script sends an email notification to a phone number via email-to-SMS gateway.

- Enhanced ease of use of TA request system which relied on manual viewing of spreadsheet to process requests
- Wrote a JavaScript script that automatically tracks activity on the course's Google spreadsheet, detecting student help requests and
sending text notifications to TAs during their shift

<div class="row">
    <div class="col-sm mt-3 mt-md-0 text-center">
        {% include figure.html path="assets/img/oh_notif_screenshot.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example notification
</div>

## How It Works

The `createSpreadsheetEditTrigger()` function creates a trigger for when a spreadsheet is edited. The script opens a specific Google Sheets file by ID using `SpreadsheetApp.openById()`. It then creates a new trigger using `ScriptApp.newTrigger()` that will execute the `alarm()` function when the spreadsheet is edited.

The `alarm()` function is triggered when the spreadsheet is edited. It retrieves the range that was edited using `e.range`, and gets the sheet using `e.range.getSheet()`. It then checks if the edited value is the same as the previous value, and if so, it returns without doing anything.

Next, it retrieves the current date and time using `new Date()`, and checks if it's during a specific time range on Sunday or Monday. If not, it returns without doing anything.

If the edited cell is in the correct column (column 3 or earlier), it retrieves the row number that was edited using `rr.getRow()`. It then retrieves data from specific cells in that row using `ss.getRange()`.

Finally, if all of the necessary data is present, it sends an email using `MailApp.sendEmail()`. The email is sent to a specific phone number (via the email-to-SMS gateway) using the `emailTo` variable, and includes the person's name, the requested assignment, and the requested time in the email body.
