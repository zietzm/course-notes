---
layout: post
title: Lab 1
permalink: /f20-symbolic/lab1
---

## Admin

There are three parts to this lab: setting up an account, connecting to the class database (plus running a quick query), and critiquing a terminology.

You're free to do this lab in whatever format and using whatever tools you think are reasonable.
Just submit a PDF on Canvas.

## Instructions

### Set up UMLS account

{% include marginfigure.html id="umls-sidefig" url="page/f20-symbolic/img/UMLS_screenshot.png" description="Example of what you should see after logging in." %}

This gives you access to tools we'll use later in the semester.

Go to <https://uts.nlm.nih.gov>, and click Sign Up (upper right corner).
Accept the license, fill in your information, and check that you can log in to the UMLS Metathesaurus Browser.

Nothing to submit for this.

### Connect to the class database

I've created a database that we'll use for several labs this semester.
{% include sidenote.html id="Database" note="It's a [MySQL 8.0](https://dev.mysql.com/doc/refman/8.0/en/) database hosted on [AWS RDS](https://aws.amazon.com/rds/).
Currently, it contains several [OMOP-formatted](https://ohdsi.github.io/TheBookOfOhdsi/CommonDataModel.html) vocabulary tables downloaded from [Athena](https://athena.ohdsi.org/)." %}


For now, let's just be sure everyone can access this database.

You're free to use whatever software you like {% include sidenote.html id="Software recommendations" note="See [software](#software) if you want recommendations." %}.
Shoot me a message if you're not able to get something installed.

The address, port, username, and password you'll use for the database will be posted on Canvas.{% include sidenote.html id="db-note" note="Couple notes:
The student account only has read access.
The DB is on a `t2.micro` free tier machine and may be a bit slow.
Please be respectful and don't run excessive queries that interfere with your classmates.
Finally, please don't share the access information for this database outside our class.
There's no PHI on there, but there's not much bandwith as is.
" %}
Once you have access, you're looking for the **`clinical_vocabulary`** database.

<span class="newthought">Your task</span> is to identify your favorite condition and tell me how many concepts use that word in their name.
For example, if you pick hypertension {% include sidenote.html id="htn" note="Pick something else." %}, you could run:

```sql
SELECT COUNT(*)
FROM CONCEPT
WHERE concept_name LIKE '%hypertension%'
```

The real point of this is to be sure everyone can access an online SQL database, so there's no need to do a fancy query.

Just tell me what condition you chose, what query you ran, and how many concepts you found.



### Terminology example

<span class="newthought">Imagine we wanted</span> to make a terminology about pizza.
Here are two such terminologies.{% include sidenote.html id="pizza1" note="I'm only going to include the first 9 of 40 types of pizza from a [diagram by Jess Kapadia](https://www.foodrepublic.com/2015/11/18/have-you-tried-these-40-types-of-pizza/)." %}


<figure>
<figcaption>Terminology 1</figcaption>
<a href="/course-notes/page/f20-symbolic/img/pizza_01.png">
<img class="fullwidth" src="/course-notes/page/f20-symbolic/img/pizza_01.png" alt="Terminology 1" />
</a>
</figure>

<br><br>

<figure>
<figcaption>Terminology 2</figcaption>
<a href="/course-notes/page/f20-symbolic/img/pizza_02.png">
<img class="fullwidth" src="/course-notes/page/f20-symbolic/img/pizza_02.png" alt="Terminology 2" />
</a>
</figure>


Please answer the following questions in your submission.
A couple sentences for each point could be sufficient.

1. Which terminology is more understandable to you, and why?
2. Which terminology do you think would be easier to add the [remaining 31 types of pizza](https://www.foodrepublic.com/2015/11/18/have-you-tried-these-40-types-of-pizza/) into, and why?
3. Can you name one advantage and one disadvantage of each terminology vs the other?
4. Can you think of any ways to improve Terminology 2?{% include sidenote.html id="pizza2" note="Don't stress too much on this one. This is one of the overall topics of the course." %}

**That's all for this lab!**

---


## Software suggestions

An easy way to test access is via the [MySQL command line interface](https://dev.mysql.com/doc/refman/8.0/en/mysql.html).
This is available for Linux/Mac package managers, and is easily installed with [Homebrew](https://formulae.brew.sh/formula/mysql), [APT](https://dev.mysql.com/downloads/repo/apt/), [pacman](https://wiki.archlinux.org/index.php/MySQL), and probably any other package manager you may be using.
Windows users could install the [MySQL shell](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-install.html).

A more familiar alternative is to use a GUI application like [Sequel Pro](https://www.sequelpro.com/), [DataGrip](https://www.jetbrains.com/datagrip/), [DBeaver](https://dbeaver.io/), or [MySQL Workbench](https://www.mysql.com/products/workbench/).

For programmatic access, I'd suggest any tool like R's [`DBI`](https://db.rstudio.com/dbi/) and [`RMariaDB`](https://rmariadb.r-dbi.org/), Python's [`sqlalchemy`](https://docs.sqlalchemy.org/en/13/dialects/mysql.html) and [`mysqlclient`](https://mysqlclient.readthedocs.io/).

Choose whatever you find most comfortable.
You can complete every lab we'll do with any of these tools.

### MySQL CLI example

The command line client is probably the easiest thing to get installed.

Once installed, use the address, port, username and password I posted on Canvas to run the following, substituting things directly.{% include sidenote.html id="CLI" note="For example, substitute `$ADDRESS` directly to `ABC123.rds.amazonaws.com`." %}

```bash
mysql -h $ADDRESS -P $PORT -u $USERNAME -p
```

You'll be prompted to enter the password.

If your access was successful, you'll see a MySQL prompt like `mysql>`.
Select the database using

```bash
mysql> USE clinical_vocabulary;
```

Then run your query.
