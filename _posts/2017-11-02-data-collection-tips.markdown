---
layout: post
title:	"Top 3 tips for collecting data with spreadsheets"
date:	2017-11-02 09:03:13 +0100
categories: data collection
---

> I wrote this post while working in the Mental Health Access Improvement Support Team ([MHAIST][MHAIST]). I've since changed employer and this modified version is reproduced here with their permission.

Opening a blank spreadsheet is a lot like beginning a New Year's resolution. With the best of intentions it's tempting to jump in and just start recording data. This may work in the short term with small data sets. But it takes a little more planning to collect data that will make a significant impact on your service.

When it come to collecting data using a spreadsheet, a small number of easy actions will save a lot of time and effort in the long run. With that in mind here are MHAIST’s top 3 tips for collecting data with spreadsheets: **keep it simple**; **document your work**; and **protect against mistakes**.

## Tip 1 - Keep it Simple

The primary objective when collecting data is managing complexity. To keep things simple: **stick with the essentials** and **keep it tidy**.

### Stick with the Essentials
**Ask yourself: do I need to collect this?** The most reliable (and easy to maintain) processes are the ones that don’t exist. Each extra data item you collect incurs an ongoing cost. So avoid the temptation to collect 'nice to have'; items: collect what you need and nothing more.

**Ask yourself: do I still need to collect this?**
Change is the only constant. So it's worth regularly reviewing whatever you’re collecting. It's not unheard of for data to be collected and reported on years after the need has passed.

### Keep it Tidy
The beauty of spreadsheets is their flexibility. But this flexibility also means they get out of control quickly; especially with multiple authors. Maintain a few simple constraints from the beginning. The time investment is minimal and you will avoid a lot of future confusion. I recommend [this paper][peerj-tidy-spreadsheets] which covers easy practical tips for tidy spreadsheets.

If this paper is a bit overwhelming try starting small. Establish tidiness for a new or small spreadsheet rather than a large or well established one. Start with a few constraints rather than all of them. For example these sections of the linked paper are a great
place to start:

* Be consistent
* Save data in rectangles
* Don’t use font colour or highlighting as data

## Tip 2 - Document your Work
The utility of numbers is their abstract nature. The corresponding risk is that numbers can easily become meaningless without sufficient context. To ensure your data remains meaningful: **create metadata** and **write (and maintain) and a README**.

### Create Metadata
Metadata is data about data. It gives context and meaning to your data. Here is an example of some dummy data and metadata:

<div style="text-align: center">
	<img src="/assets/metadata.png" alt="two rows of dummy data with a data dictionary to the right"/>
	<p></p>
</div>

Meta data encompasses the extra columns such as **Record_Date** and the field descriptions to the right (this section is often called a data dictionary). Meta data makes life easier for colleagues and your future self. Some metadata items like unique identifier or date of entry may not seem immediately useful. However metadata often becomes useful (and even essential) months or years down the line. Sometimes in unforeseen ways. For example:

* Unique Identifiers are useful when moving data to a different system like a data base
* CHI is a nationally-recognised unique identifier which can be used to link your data to other data sets
* Date of Entry can help find and correct data entry errors

### Write (and maintain) a README
The README is a simple concept borrowed from the software development industry. Create a file (maybe a tab in your spreadsheet) called README. Use this to answer basic questions like: *Why is this data being collected? Who asked for it in the first place? Who built this process and how do I find them?* A good README is comprehensive yet brief; often a single page. It’s written for humans and is therefore **readable**.

**Make your README readable**. It takes cognitive effort to condense sentences. And the average reading age of the UK population is [9 years][readability]. So writing long sentences effectively offloads that cognitive work onto your audience. This is especially significant because documents are usually read more times than written. Keep it short and sweet. Make it scan-able with subtitles and bullet points.

## Tip 3 – Protect Against Mistakes

A robust data collection process is resistant to random variation. Protect against mistakes and accidents such as: **clumsy fingers**; **inappropriate data entry**; and **IT and human error**.

### Clumsy Fingers
Manual typing is error prone so it pays to be picky about what you accept into your data set. Make it physically impossible to add the wrong type of information to your spreadsheet. Excel 2007 has a data validation feature that looks like this:

<div style="text-align: center">
	<img src="/assets/excel-validation.png" alt="Excel data validation window"/>
	<p></p>
</div>

Where possible set this up for each column in your data set - Excel will complain if you try to enter an invalid data point:

<div style="text-align: center">
	<img src="/assets/excel-validation-error.png" alt="Excel data validation error window"/>
	<p></p>
</div>

Use this feature to restrict both **types** and **values**. Make it impossible to input a name into a date column (wrong type). A value like **NHS Kothian** shouldn’t be allowed in a Health Board column (impossible value).

### Inappropriate data entry
Usually the risk of malignant data entry is minimal. A more significant issue is well intended (but misguided) data entry. One option is to protect your data sheets with a password. In Excel it looks like this:

<div style="text-align: center">
	<img src="/assets/excel-protection.png" alt="Excel password protect window"/>
	<p></p>
</div>

Passwords can be used to restrict access to a file. But they can be used in other ways too. For example, try saving the password within your file; perhaps intentionally at the end of documentation. Rather than restricting access, this serves as a reminder of the documentation each time the spreadsheet is changed. Of course, all this assumes that your spreadsheet is already secure without needing a password.

### IT and human error
Clumsy fingers and inappropriate data entry can cause the wrong data to be recorded. Another risk is losing the right data; often due to IT and human error. To minimise this risk: **regularly back up your data** and **never delete anything (within reason)**.

* **Regularly back up your data**. Backing up occasionally is better than nothing. A backup schedule with copies in multiple locations is even better.
* **Never delete anything (within reason)**. An alternative to deleting a row of data is to include a “deleted” or “ignore” column. Fill this column with values like TRUE/FALSE, or "Active"/"Inactive". This reduces the risk of deleting the wrong thing.

[MHAIST]: http://www.isdscotland.org/Health-Topics/Mental-Health/MHAIST/
[MHAIST-ihub]: http://ihub.scot/a-z-programmes/mental-health-access/
[MHAIST-twitter]: https://twitter.com/his_mhaist
[peerj-tidy-spreadsheets]: https://peerj.com/preprints/3183.pdf
[readability]: http://www.see-a-voice.org/marketing-ad/effective-communication/readability/