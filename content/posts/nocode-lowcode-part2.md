---
title: Building a Low-Code/No-Code Data Engineering Framework - Part II
date: 2023-08-07
description: Learn about the inception of our unique framework, designed to streamline and democratize the data engineering process. Understand how this innovation in data engineering has enhanced our development workflow, promoting efficiency and collaboration. However, innovation isn't without its challenges.
disableComments: false
showHero: true
tags:
  - dataengineering
  - databricks
---

In our inaugural exploration ([[nocode-lowcode-part1|Part 1]]), we embarked on a journey, diving into the foundational aspects and transformative potential of a Low-Code/No-Code [[data_engineering|Data Engineering]] approach. As we venture deeper in Part 2, we'll unravel the intricacies of the No-Code [[data_engineering|Data Engineering]] framework, shedding light on its robust architecture and configuration-driven design. We briefly touched upon how this framework has potential to democratize [[data_engineering|Data Engineering]] , making it accessible to both technical maestros and novices alike. As we forge ahead in Part 2, our expedition delves deeper, unraveling the layers that constitute the Low-Code/No-Code [[data_engineering|Data Engineering]] realm.

The framework's robust architecture is really simple. Built on principles of Configuration-Driven Design, it is crafted to be malleable, catering to varied data needs while ensuring the integrity and efficiency of the [[data_pipeline|Data Pipeline]]. The paradigm of No-Code/Low-Code [[data_engineering|Data Engineering]] is not merely about the absence of coding; it's about optimizing processes, streamlining workflows, and, most importantly, bridging the chasm between technical and non-technical users. This is where its user-friendly interface will shine, acting as a beacon for those venturing into data realms previously deemed insurmountable without a coding background.

Platforms like reddit have become hotbeds of discussions, teeming with enthusiasts and skeptics alike, dissecting the merits and challenges of [[data_engineering|Data Engineering]] sans the traditional coding rigmarole **[TODO: Add links supporting this]**. But what truly sets this platform and software apart? Beyond the surface-level allure of simplicity, this platforms harbor intricate mechanisms. From extensible [[data_pipeline|Data Pipeline]]s that ensure seamless data transformation to the embedded good coding practices ensuring the system's reliability, the depth of this framework is astounding.

Since the logic of the [[data_pipeline|Data Pipeline]]s has been already wrapped in neatly packaged classes and have already been unit tested thoroughly, the significance of unit testing in traditional frameworks becomes less pressing in this No-Code paradigm. Developers no longer have to invest extra time in unit testing on their end. Ensuring that every module functions as intended, that every cog in the machine runs smoothly, becomes a given. This not only streamlines the development process but also provides assurance of the system's reliability. Add to this the principle of extensibility, and you have a framework that is not only robust at its core but also adaptable, ready to evolve with the ever-changing data landscape, giving developers more time to engineer effective solutions.

Whether you're a seasoned data engineer, a budding enthusiast, or someone merely intrigued by the buzz surrounding low code platforms or no code platforms, this exploration promises insights and revelations. As we navigate through the intricacies of the framework, from its architecture to its operational nuances, join us in discovering the future of data engineering—a future where complexity is tamed, and innovation thrives.

## The Architecture

Let me explain how I came up with the Architecture of this framework.

### Framework Architecture - The Ideation

When embarking on the journey to design a robust [[data_engineering|Data Engineering]] framework, it's crucial to lay a strong architectural foundation. Let's delve into the intricate architecture of our No-Code/Low-Code [[data_engineering|Data Engineering]] framework.

#### 1. Data Assumptions and Environment

The framework operates on a fundamental assumption: the data you're processing is already within your working environment. In the context of my organization:

- Primarily, our data resides in **Azure Datalake** or **Azure SQL Server**. These platforms cater to over 90% of our team's use cases. However, the beauty of this framework is its extensibility. Theoretically, it can integrate with any service accessible via Azure Databricks, as our pipelines execute within this environment.
- Post-processing, we typically store datasets within the Azure ecosystem. Whether it's Azure Datalake or Azure SQL Server, these platforms seamlessly integrate with our frontend applications.
- Our design philosophy revolves around the **Lakehouse** model. We've adopted the **Medallion Architecture** for data storage. Here's a snapshot: One team pushes data into a `RAW` folder. From there, data transitions to the `PROCESS` folder, and finally, it finds its resting place in the `OUTPUT` folder.

#### 2. The Three Pillars: Read, Transform, Write

Upon a closer inspection of our [[data_pipeline|Data Pipeline]]s, a pattern emerges. Regardless of the complexities and nuances, at their core, these pipelines revolve around three primary stages: Reading, Transforming, and Writing data.

- The sequence of these stages can vary. For instance, the ETL (Extract, Transform, Load) process follows a Read-Transform-Write sequence. In contrast, ELT (Extract, Load, Transform) involves Reading, Writing, then Transforming, followed by another Write operation. Some specialized pipelines might even adopt a Read-Transform-Write (for rejected datasets)-Write (for final datasets) sequence.
- With these diverse scenarios in mind, and anticipating future variations, I encapsulated the dataset representation within a Python Class named `SparkDataset`. This class serves as the backbone of our data operations. As for the pipeline representation, it's elegantly captured using dedicated classes like `ETL`, `ELT`, and others, ensuring flexibility and adaptability.

Keeping all these things in mind, this is the final Class UML for the entire
framework. This is how the final Class UML diagram looks for the framework.

![[Framework - Class UML.png]]

Obviously, this is not an exact representation of what we are using in our organization. But this gives a fair idea of what we have implemented. Looking at this, you should have a rough idea about how this can be further extended.

### Diving Deeper - `SparkDataset` Class

Having explored the foundational layer of our framework's architecture, it's time to delve into the second layer, where the magic truly happens - the `SparkDataset` class.

#### 1. Core Functions of `SparkDataset`

The `SparkDataset` class is elegantly simple, yet powerful, comprising just three primary functions:

- **Initialization (`__init__`)**: He we prepare the `SparkSession` object, ensuring we're ready to dive into data operations.
- **Reading (`read()`)**: As the name suggests, this function is all about ingesting data, reading it into a PySpark dataframe.
- **Transformation (`transform()`)**: This is where the data undergoes metamorphosis. Based on the configurations specified, this function applies a series of transformations to shape the data as required.
- **Writing (`write()`)**: The final act. Once the data is processed and refined, this function ensures it's written to the desired destination.

#### 2. The Flexibility Factor

But that's just the tip of the iceberg. The true versatility of the `SparkDataset` class lies in its adaptability:

- **Diverse Data Formats**: Our data sources are as varied as they come. From CSV, parquet, and delta formats to the occasional Excel file (though we're not big fans), and even datasets housed in Azure SQL Server. The class gracefully handles these varied formats.
- **Writing Capabilities**: Similarly, when it comes to data output, whether you're looking to write data as parquet, delta, or load it into Azure SQL Server, `SparkDataset` has got you covered.
- **Limitless Transformations**: The sky's the limit when it comes to data transformations. Whether you're applying just one or a whopping fifty transformations, the class handles it with ease.

#### 3. The Extensibility Enigma

I've often emphasized the extensibility of this framework. But how did we achieve this without compromising on functionality? The secret sauce lies in the design of the `SparkDataset` class. Instead of embedding specific logics for reading, writing, or transforming data within the class, we've externalized them into separate classes. Through the power of [[Class Composition]], we plug in the necessary classes based on the use case. Here's a glimpse of how we can instantiate a `SparkDataset` object:

```python
dataset = SparkDataset(config="some_config.yaml")
dataset.read(reader=SQLServerReader)
dataset.transform(transformation_key="transformation")
dataset.write(writer=DataLakeWriter)`
```

With this approach, you can effortlessly swap out classes for reading and writing. And given that multiple transformations are often the norm, we pass a LIST of Transformations defined in the configuration file (like "some_config.yaml").

#### 4. User-Driven Evolution

One of the core tenets of our framework is its **adaptability**. We envisioned a system that's not just robust in its current form but is also malleable enough to **evolve** with the ever-changing landscape of data engineering.

Imagine a scenario where a user, perhaps from a different team or even a different organization, has a unique requirement. Let's say they need to read data from Postgres SQL. Instead of waiting for the original developers to update the framework or resorting to cumbersome workarounds, they should be able to seamlessly integrate this new functionality. The same principle applies to transformations and data writing.

To achieve this level of flexibility, we needed a well-thought-out approach. The answer lay in one of the foundational design patterns in software engineering - the [[Strategy Design Pattern]]. By leveraging this pattern, we've created a framework where functionalities can be extended or swapped without altering the existing codebase. It's like adding new tools to a Swiss Army knife; each tool (or strategy) is independent but integrates perfectly with the overall mechanism.

### Decoding the Reader and Writer Classes

The beauty of our framework lies in its simplicity and structure. By using the Strategy Design Pattern, we've ensured that adding new functionalities or tweaking existing ones is a breeze. Let's delve deeper into how this is achieved, particularly for our Reader classes. (And remember, the same logic applies to our Writer classes too!) The Blueprint: Abstract Reader Class

At the heart of our Reader functionality is an abstract class, which essentially serves as a blueprint for all subsequent Reader classes. This abstract class, DataReader, doesn't perform any operations by itself. Instead, it lays down a set of rules or protocols that every Reader class must adhere to.

Here's a peek into its structure:

```python
from abc import ABC, abstractmethod
from pyspark.sql import SparkSession, DataFrame

class DataReader(ABC):

	def __init__(self, spark: SparkSession) -> None:
		self.spark = spark

	@abstractmethod
	def read(self, input_path: str, input_format: str, options: dict[str, Any]) -> DataFrame:
		raise NotImplementedError()
```

The `DataReader` class mandates two primary features for all its child classes:

1. **Configuration Options**: Accept configuration parameters from the config file.
2. **Data Reading Function**: A function that reads data and returns a Spark DataFrame object.

#### DataReader In Action: `DataLakeReader`

Building upon the foundation laid by the `DataReader` class, let's look at a concrete implementation: the `DataLakeReader` class.

```python
class DataLakeReader(DataReader):

	def read(self, input_path: str, input_file_type: str, file_read_options: dict[str, Any], **kwargs) -> DataFrame:
		try:
			df_data = (
				self.spark.read
				.format(input_file_type)
				.options(**file_read_options)
				.load(input_path)
			)
			return df_data
		except Exception as err:
			raise FileReadException(f"Error occurred while reading the file: {err}")
```

This class, while adhering to the protocols of the abstract class, provides a specific implementation for reading data from a data lake. It's designed to be robust, handling potential errors gracefully.

#### Writers: A Mirror Reflection

The Writer classes follow a similar structure. At their core, they have an abstract class that defines the rules. Each specific Writer class then provides its unique implementation, ensuring data is written seamlessly to the desired destination.

## Extensibility - The Power to Evolve

As we continue to delve deeper into the architecture of our No-Code/Low-Code [[data_engineering|Data Engineering]] framework, one of its defining features is its remarkable extensibility. This aspect empowers the framework to adapt and evolve, catering to a wide array of [[data_engineering|Data Engineering]] requirements.

We've already explored the core functions of the `SparkDataset` class, which forms the backbone of our data operations. But what truly sets it apart is its inherent flexibility.

### Diverse Data Formats

In the world of data engineering, diversity is the norm. Our data sources come in various formats, from CSV and Parquet to Delta, and occasionally even the less favroured Excel files. With the `SparkDataset` class, this diversity is embraced, as it gracefully handles an array of data formats.

### Writing Capabilities

Similar to its prowess in reading data, the `SparkDataset` class excels in writing data as well. Whether you need to write data as Parquet, Deleta, or load it into Azure SQL Server, this class is ready to meet your data output needs.

### Limitless Transformations

Data Transformations is wheer the magic happens, and the `SparkDataset` class is a magician's wand. Whether you're applying one transformation or a complex sequence of fifty, this class handles it with ease, adapting to your data transfromations.

### Feature Engineering Made Easy

One of the core tasks in [[data_engineering|Data Engineering]] is feature engineering. This process involves creating new features from existing data, transforming raw data into informative features that machine learning models can use for prediction and analysis.

The `SparkDataset` class simplifies feature engineering by providing a range of built-in functions and utilities for commmon feature engineeering tasks. Whether you need to create a new columns, apply mathematical transformations, or handle missing data, the class offers a user-friendly interface to perform these operations effortlessly.

### Streamlining Data Science Models

As organizations grow and [[data_engineering|Data Engineering]] pipelines become more complex, the need to streamline the integration of Data Science Models into the framework becomes apparent. When teams create hundreds of models, patterns tend to emerge, and repetitive tasks can be automated.

The future of our framework includes a dedicated module for Data Science Model integration. This module will facilitate the seamless incorporation of machine learning models, allowing data engineers and data scientists to collaborate efficiently. Whether it's deploying models in batch processes, automating model evaluation, or managing model versions, our framework will simplify these processes, reducing the overhead of managing a growing model ecosystem.

Stay tuned for more insights into how our No-Code/Low-Code [[data_engineering|Data Engineering]] framework continues to evolve and adapt to the ever-changing landscape of [[data_engineering|Data Engineering]] and data science.

## Conclusion

As we conclude our journey through the architecture of our No-Code/Low-Code [[data_engineering|Data Engineering]] framework, it's clear that the power to evolve is at the heart of its design. This framework isn't just a static solution; it's a dynamic and adaptable tool that grows alongside your [[data_engineering|Data Engineering]] needs.

From handling diverse data formats to simplifying feature engineering and envisioning the seamless integration of Data Science Models, our framework is a testament to the ever-evolving landscape of [[data_engineering|Data Engineering]] and data science.

We invite you to embrace this future of data engineering—a future where complexity is tamed, innovation thrives, and collaboration between technical maestros and novices becomes the norm. Our journey doesn't end here; it continues to evolve, just like the data landscape it serves.

Stay tuned for more insights, updates, and innovations as we embark on this exciting expedition through the world of data engineering. Together, we'll continue to shape the future of data.

Thank you for joining us on this exploration, and we look forward to the adventures that lie ahead in the world of data.
