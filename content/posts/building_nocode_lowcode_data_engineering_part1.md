---
title: "Building a Low-Code/No-Code Data Engineering Framework: A First-Hand Experience - Part I"
date: 2023-07-30T17:01:43+05:30
description: "Explore the transformative potential of Low-Code/No-Code Data Engineering in this detailed blog post. Learn about the inception of our unique framework, designed to streamline and democratize the data engineering process. Understand how this innovation in data engineering has enhanced our development workflow, promoting efficiency and collaboration. However, innovation isn't without its challenges."
image: images/markus-spiske-code-faded-unsplash.jpg
imageAltAttribute: "Fuzzy Code"
disableComments: false
tags:
  - Data Engineering
  - Databricks
---

Let's dive into the world of Low-Code/No Code Data Engineering. But before we
do, let's set the stage with a bit of context on the Data Engineering Process.

Traditional data engineering is a complex and intricate process. It involves
creating and maintaining architectures, databases, and processing systems that
deal with vast amounts of data. Think of Data Engineers as the architects of
data. They build pipelines that transform and transport data into a format that
can be used by data scientists. They are the ones who ensure the data is clean,
reliable, and prepped for analysis. But this process is often time-consuming and
requires a high level of technical expertise, which hampers the Development
Workflow.

Enter [Low-Code](https://www.wikiwand.com/en/Low-code_development_platform)
[No-Code](https://www.wikiwand.com/en/No-code_development_platform), an
innovation in Data Engineering. I believe that this approach can simplify the
process of data integration and processing. It allows individuals without a deep
technical background to build and manage data pipelines. With a no-code
platform, you can design your data workflows visually and automate the data
pipeline without writing a single line of code. It's like having a magic wand
that turns complex data tasks into a series of simple, intuitive steps.

Now, you might be wondering why I, a humble blogger, decided to embark on the
journey of creating a No Code Data Engineering platform. Well, it's simple. I
saw the challenges that traditional data engineering posed and I wanted to make
a difference. I wanted to democratize data engineering by making it accesible to
all. But, as with all great endeavors, there were bumps along the road. I faced
failures and there were times when I wanted to throw in the towel. But every
failure was a lesson learned and every setback, a stepping stone towards
progress.

## Why Low-Code/No-Code Data Engineering?

### Why are Companies Moving Towards a Low-Code/No-Code Approach for Data Engineering?

Firstly, let's talk about the **Democratization of technology**. Both low-code
and no-code solutions are built with the objective of empowering different kinds
of users. As [IBM](https://www.ibm.com/cloud/blog/low-code-vs-no-code) puts it,
these platforms are designed to make technology accessible to a wider audience,
not just those with extensive coding skills. The importance of democratizing
technology lies in its potential to foster widespread innovation, creativity,
and problem-solving capabilities. By breaking down the barriers of technical
complexity, these platforms enable a more diverse pool of minds to engage in
technological exploration. A Javascript Developer, a newbie IT Analyst, and
individuals with non-technical backgrounds can now actively contribute to the
development of innovative solutions without the need for extensive coding
knowledge. This democratization nurtures a culture of collaboration and
inclusivity, where ideas from various perspectives converge, leading to the
emergence of novel applications and cutting-edge advancements. This shift is
breaking down barriers between technical and non-technical personnel. I've
always held the belief that a product cannot truly succeed unless business users
take an active interest in their IT solutions. In the context of data
engineering, this perspective becomes even more crucial.

Another reason for choosing a low-code/no-code platform is the **speed and
efficiency** it offers. As
[Zapier](https://zapier.com/blog/low-code-vs-no-code/) points out, no-code
development is the fastest way to build and create solutions. It's also the most
cost-effective and easiest to maintain over time. Using this framework which we
have built, one of our junior developer has significantly improved his
development speed. He has been delivering pipelines at a phenomenal speed.

### My Reasons for Moving to Low-Code/No-Code Setup

Imagine you're part of a relay race. You're running at breakneck speed, passing
the baton, and just when you think you're about to cross the finish line, you're
told to run the race again, but this time, backwards. That's what it feels like
working in our fast-paced environment. We're juggling data gathering,
exploratory data analysis, machine learning model creation, and oh, did I
mention, we're also expected to whip up a high-quality data pipeline in the same
breath? No extensions. It's like being asked to bake a cake while simultaneously
performing a ballet. And guess what? 80-90% of our time is spent on tasks that
have nothing to do with data engineering.

In the midst of this whirlwind, we often find ourselves creating what I like to
call the 'Frankenstein's Monster' of code. It's either a '[God
Object](https://en.wikipedia.org/wiki/God_object)', a class that's bitten off
more than it can chew, a '[Spaghetti
Code](https://en.wikipedia.org/wiki/Spaghetti_code)', a tangled mess that's as
flexible as a brick, or a big '[Ball of
Mud](https://de.wikipedia.org/wiki/Big_Ball_of_Mud)', a code so convoluted that
even Sherlock Holmes would have a hard time deciphering it. And these aren't
just fancy terms I'm throwing around; they're real [Anti-Design
Patterns](https://en.wikipedia.org/wiki/Anti-pattern) that haunt our
deliverables.

<figure>
  <img src="https://i.imgflip.com/7ufo3p.jpg" title="God Object" alt="God Object Meme">
  <figcaption>
  	<em><center>This is how a God Object works</center></em>
  </figcaption>
</figure>

Now, let's talk about the wild west of **coding styles** in our company.
Everyone's a cowboy, riding their own horse, following their own trail. It's
like trying to understand an orchestra where every musician is playing a
different tune. It's a nightmare for our Lead Engineers and Architects who have
to review these 'masterpieces'.

And then there's the issue of **standardization**, or rather, the lack of it.
It's like everyone's cooking their own version of a classic recipe. Take '[Base
Price](https://analyticsstudent.wordpress.com/2012/10/31/baseline-sales-for-marketing-mix-modeling/)'
in Media/Marketing Mix Modeling, for example. You'd think it's a standard
calculation, right? Wrong. Every team has their own secret sauce, which works
great for their dish but falls flat in others.

Lastly, let's not forget the elephant in the room - **good coding practices**.
Or in our case, the lack thereof. It's like everyone's so busy juggling, they've
forgotten to check if the balls they're juggling are even round. **Unit
testing**? What's that? We're so caught up in writing functions for specific
tasks that we've forgotten to make them reusable, let alone testable.

So, these are my main pain points. It's a wild ride, but hey, who said data
engineering was going to be a walk in the park? I would really like to have a
Clean Code book just for Data Engineering/Data Science.

## Desired Features from the Framework

Imagine you're handed a magic wand that can transform complex data engineering
tasks into a walk in the park. Sounds too good to be true, right? Well, that's
exactly what I envisioned when I set out to create this Framework. Let's take a
peek into the magic box of features I had in mind.

### User-Friendly Interface and Configuration-Driven Design

The first thing I wanted to conjure up with my magic wand was a user-friendly
interface. I decided to start with the heart of the system - the code packages.
The idea was to create a robust foundation first and then wrap it up with a
pretty bow, aka the User Interface. The entire data engineering pipeline was to
be defined as a configuration file. This file would be the master key, unlocking
the source input file, defining its properties (CSV, Excel, Parquet, Delta
format, you name it), and setting the parameters for reading the data.

Once the source dataset was read as a PySpark Dataframe, the configuration file
would guide the transformations, validations, and finally, the write command.
Now, I know what you're thinking. This configuration file could potentially
become as long as a Tolstoy novel. And you're right.

I started off with JSON for the configuration file, but it soon started to
resemble a plate of spaghetti with all the nested configs. So, I switched to
YAML, which made the configuration file a bit more readalbe, if you would as me.
Here's a sneak peek into one of the configuration files for a data pipeline.

```yaml
source:
  dataset_name: Sample Dataset
  read_path: <path to the file/folder location>
  read_format: parquet
  read_options:
    inferSchema: true

transformations:
  - stage_name: SelectColumnTransformer
    comment: Selecting only the required columns
    args:
      columns:
      - Country
      - State
      - City
      - Year
      - Population

  - stage_name: ColumnTransformer
    comment: Correct the values in Country Column
    args:
      columns:
      - column: Country
        expr: "CASE WHEN County = 'India' THEN 'IND' ELSE Country END"
      - column: Year
        expr: "int(Year)"

  - stage_name: GroupByTransformer
    comment: Get Aggregated values
    args:
      group_by:
       - Country
       - State
       - Year
      aggregations:
        Min_Population:
          column: Population
          agg: min
        Max_Population:
          column: Population
          agg: max
        Total_Population:
          column: Population
          agg: sum

write:
  file_name: <File Name>
  file_path: <Path to write>
```

I don't know about you, but this is pretty in my eyes. It looks prettier in a
proper Text Editor as well. And yes, I hear you. This is still a configuration
file, and someone has to write these configurations down. But hey, Rome wasn't
built in a day. This was just the first step. Once I was happy with the
framework, the plan was to work on creating a user-friendly interface with all
the bells and whistles.

I know, I know, I could've started working on it in parallel. But here's a
little secret: I don't know how to create a GUI with drag and drop
functionalities.

### A One-Stop-Shop for Data Reading, Transformation, and Writing

This framework is a toolbox, which has each and every tool which is designed to
perform a specific task in a given data engineering process. That's exactly what
I envisioned for my Low-Code/No-Code Data Engineering Framework.

Data engineering, in its essence, is a series of tasks that can be broken down
into smaller functions. Reading a single CSV file or multiple CSV files, reading
Excel or Parquet files, fetching data from Microsoft SQL Server or Snowflake -
these are all individual tasks. Then come the transformations - selecting
columns, grouping by, ordering by, pivoting, unpivoting, filtering, adding or
removing columns, and so on. Finally, we have the writing options - outputting
the data as CSV, Parquet, Delta, or write to SQL. In my eyes, data engineering
is just these steps happening in various permutations and combinations from a
desired list.

So, I placed each of these small units in a class, which is then called in the
main pipeline. This approach has two main advantages:

**1. Extensibility**: This is the biggest advantage. Let's say someone wants to
add a new functionality. With this framework, it's as simple as adding a new
class for that particular functionality. This modular approach makes the system
highly adaptable and scalable. It's like playing with Lego blocks - you can keep
adding, removing, or rearranging the blocks to create whatever structure you
want. The same goes for our data engineering tasks. Need a new transformation
function? Just create a new class. Need to read data from a new source? Add a
class for that. The possibilities are endless.

**2. Good Coding Practices and Unit Testing**: The second benefit is that the
data engineer using this framework doesn't have to worry about good coding
practices or unit testing - all of that is already taken care of in the
framework. It's like having a safety net. The developers just have to focus on
writing pipelines and defining validation steps. This significantly reduces the
cognitive load on the developers and allows them to focus on what they do best -
engineering data.

# Stay Tuned for the Next Chapter

As we turn the page on this chapter, I'm thrilled to share that our story of
building the Low-Code/No-Code Data Engineering Framework isn't a tale of
fiction. It's a reality, it's tangible, and it's ready to be put into action.

But don't close the book just yet! We're merely at the end of a chapter, not the
whole story. We've set the scene for a new development workflow and introduced
our characters. Now, it's time for the plot to thicken.

In the next chapter (or rather, the next article), we'll delve deeper into the
heart of the narrative. We'll explore the intricacies of the code, the twists
and turns of our journey, the challenges we faced, and how we overcame them.
We'll also share the reviews and feedback from the brave team members who've
been using this framework, and see whether this has really democratized data
engineering processes or not!

So, keep your bookmark ready, sit back, and get ready for the next chapter. What
are you most excited to learn about in our journey?

# References

Here are some articles that I found extremely helpful in my journey and I hope
they will be for you too:

- [Low-Code or No-Code: What's the Difference](https://www.ibm.com/blog/low-code-vs-no-code/):
This blog on IBM's blog provides a comprehensive comparison between low-code and
no-code development platforms. It explains how both platforms aim to democratize
technology and increase productivity by abstracting complex coding aspects, but
they target different user groups and use cases, with low-code offering more
customization and scalability for professional developers, while no-code
provides a completely hands-off approach suitable for business users and
straightforward applications.

- [Code vs Low Code vs No Code: When to use each one](https://zapier.com/blog/low-code-vs-no-code/):
This blog on Zapier's blog provides a detailed comparison of full-code,
low-code, and no-code platforms, discussing their pros, cons, and ideal use
cases. It emphasizes that while full-code allows for ultimate customization,
low-code and no-code platforms offer faster, more cost-effective solutions that
are easier to maintain and adapt, making them increasingly attractive for
businesses looking to streamline development and processes.

- [The Future of Data Engineering is No-Code](https://www.datameer.com/blog/no-code-future-of-data-engineering/):
This article discusses how the rise of no-code tools is streamlining data
engineering processes and driving down costs. It emphasizes that these tools not
only enhance agility but also allow team members to participate more actively in
development processes, thus breaking the data engineering logjam and fostering
efficient and agile data engineering processes.

- [No-code data engineering solutions](https://www.reddit.com/r/dataengineering/comments/nx65fa/nocode_data_engineering_solutions/):
This is a lively discussion among data engineers about the pros and cons of
no-code and low-code solutions for data engineering tasks. Participants share
their experiences with a variety of tools, including SSIS, ADF, and Matillion,
and discuss the benefits and limitations of no-code ETL solutions like Stitch.
The thread also includes a healthy debate about the practicality and efficiency
of these tools, with some users expressing skepticism about their long-term
viability and others advocating for their potential to streamline data
engineering processes and democratize data handling.

- [Data Engineering Career Path: To Code or not to Code](https://dataexpert.medium.com/data-engineering-career-path-to-code-or-to-no-code-1f09cd30552a):
This personal blog on Medium discusses the author's personal journey as a Senior
Data Engineer and the varying perceptions of Data Engineering roles across
different companies. The author notes that **many companies view their Data
Engineers as an extension of analytics, while others see them as an extension of
Software Engineering**. The author believes that the divide in the perception of
Data Engineering roles has been caused by excellent data platform products from
companies like DBT, Snowflake, DataDog, Palantir, and DataBricks. These tools
empower SQL-specialists to handle tasks that were previously relegated to
Software Engineers or Data Engineers.
