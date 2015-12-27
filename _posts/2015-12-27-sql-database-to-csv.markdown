---
layout: post
title:  "Exporting SQL data into CSVs via Powershell"
date:   2015-12-27 06:44:27 -0600
categories: tools sql powershell
---

I've been working on an integration component for a web app with a team of developers. This system is supposed receive data from multiple disparate systems. In once case in particular, we really wanted some sample data from the company that was going to be passing us data to our API to better understand what some of the incoming data could look like.

### The Problem


<img src="https://i.imgur.com/iWKad22.jpg" alt="facepalm" style="margin: 1em; float: right; max-width: 40%;" />
Since I had been traditionally the one to communicate with our liaison to this company. I asked him if he could provide us with something in the way of sample data and he obliged, albeit in an unexpected way. After one day passed, I received a zip file via Google Drive share link. I opened it up and found that he had simply exported a very large backup of the system's SQL Server database. Some of my teammates who were CC'd on the email thread noticed the ominous ".bak" file and scornfully remarked "What the heck is that file?!", understandably so, as most hadn't worked on anything in the Microsoft / .NET stack at all.

So it was up to me to get some viewable sample data out of this to my teammates who had no other way of viewing it, being on Macs with no Windows VM or Bootcamp setup. My first thought was to dump all of the tables into CSV files. Since we've received sample data in this format in the past and everyone was comfortable with it, that's the route I took.

### The Options

I needed to figure out a fast way to get all of tables in this SQL Server backup into CSVs. The first step, of course, was to restore them into my local SQL Server instance. After that, I thought about a few different ways to accomplish the task. In addition to getting this data quickly, I hoped to find an easily reusable way to do this, because I've seen this scenario come up before. I knew that I could easily get CSVs out of a SQL Server Database with SSIS, which I've had extensive experience with in the past. However, it's time consuming and not easily made reusable. I also seem to recall the "Export Data" dialog in SQL Server being able to handle tasks like this, but I also remember it being unwieldy and having to setup awkward datasources similar to SSIS. My final thought and the solution I chose was to write a fairly simple Powershell script.

### The Solution

I knew it would be fairly trivial to make the script reusable. I had used Powershell commandlet in the past that allows piping objects into CSVs, and it only took about 15 minutes to refresh my knowledge of how to select objects from SQL Server database using Powershell. In a few minutes I had a working script and was able to get the output files passed off to my teammates.

{% highlight powershell %}
$database = 'MyDatabaseName'
$instance = 'localhost\SQLEXPRESS'

$tables = Invoke-SqlCmd -Query "SELECT TABLE_NAME FROM [$database].INFORMATION_SCHEMA.Tables" -ServerInstance $instance -Database 'msdb'
foreach ($table in $tables) {
  $tableName = $table.TABLE_NAME
  Invoke-SqlCmd -Query "SELECT TOP 50 * FROM [$tableName]" -ServerInstance $instance -Database $database |
  ConvertTo-Csv -Delimiter '|' -NoType |
  ForEach-Object {$_.Replace('"','')} |
  Out-file "C:\DATA\$tableName.csv"
}
{% endhighlight %}

I'm sure that there are more concise or elegant ways of solving this problem, but this is the route I chose based on my knowledge of the tools available and time constraints. I'm quite pleased that the script is fairly simple and reusable. I encourage anyone who has alternative methods to post in the comments thread below. I would love to hear your ideas.
