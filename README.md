## Replication Package: Detecting Code Smells using ChatGPT: Initial Insights


### Replication Package

This repository contains data files to replicate our study presented in the paper *"Detecting Code Smells using ChatGPT: Initial Insights"*.

### Dataset Structure

We provide raw and preprocessed data in different formats: 

* **csv** - the database in CSV format with comma separated columns.
* **csv-semi-comma** - the database in CSV format with semi-comma separated columns.
* **html** - the database in HTML format to ease the visualization of the dataset. 
* **sql** - the original SQL (schema and data) of the database used in this study.

Each compressed directory contains a README file explaining which information each column includes. 

### Dataset Overview

A. **`sql`** directory consists of two tables: 

1. The table `tb_unique_bad_smell` contains information we collect from ChatGPT.  

```sql=
CREATE TABLE public.tb_unique_bad_smell (
    id_unique_bad_smell integer NOT NULL,
    id_bad_smell bigint,
    id_source_code bigint,
    chat_gpt_response text,
    question text,
    badsmell_base text,
    bad_smell_gpt text,
    found_any boolean,
    valid_bad_smell boolean,
    bad_smell_in_base boolean,
    bad_smell_not_in_the_base text,
    bad_smell_not_found text,
    index integer,
    index_base integer,
    url_github text,
    id_base bigint,
    dt_insertion timestamp without time zone,
    nr_question smallint
);
```

* **`id_source_code`** - integer identifier when we imported the original dataset to our database.
* **`chat_gpt_response`** - contains ChatGPT's response to our prompts. 
* **`question`** - This column contains all the prompts we submitted to ChatGPT. Each question includes the prompt under evaluation and the source code we were interested in evaluating.
* **`badsmell_base`** - code smells assigned in the original dataset. 
* **`bad_smell_gpt`** - code smells identified by the ChatGPT. We extracted these smells from `chat_gpt_response`.
* **`found_any`** - a boolean field indicating if any of the smells found by ChatGPT are in the dataset. In other words, if ChatGPT answered yes, finding any smell (even if it is not in the original dataset).
* **`valid_bad_smell`** - text field containing the smells in the original dataset that the ChatGPT identified.
* **`bad_smell_in_base`** - a boolean field indicating if the smells found by ChatGPT are in the original dataset.
* **`bad_smell_not_in_the_base`** - text field containing the smells that ChatGPT found and they are not in the dataset. 
* **`bad_smell_not_found`** - text field containing the smells in the dataset that ChatGPT did not detect.
* **`index`** and **`index_base`** - indexes imported from the original dataset. GitHub provided them.
* **`url_github`** - the GitHub URL of the source code extracted from the original dataset. 
* **`id_base`** - id field in the original dataset.
* **`nr_question`** - integer field containing 1 or 2, identifying the prompt we submitted to ChatGPT. 


2. The table `tb_unique_source_code` contains information we imported from the original dataset we used to submit to ChatGPT and information to evaluate ChatGPT's performance. The primary data we relied on are:


* **`smell`** - presents the smell assigned to the code.
* **`severity`** - the severity of the smells, Major, Critical, Minor. 
* **`type`** - function or class.
* **`code_name`** - the full path for the smell, e.g., `nm_package.nm_class.nm_method`
* **`start_line`** - the code where the smell starts.
* **`end_line`** - line in the code where the smell ends.
* **`link`** - the GitHub URL of the source code evaluated.

