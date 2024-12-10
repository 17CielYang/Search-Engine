# Search-Engine

A simple and extensible search engine implemented in Java that indexes and searches various document formats including PDF, Word, HTML, and PNG. It leverages powerful libraries such as [ApacheLucene](https://lucene.apache.org/), [ApacheTika](https://tika.apache.org/), and [Jsoup](https://jsoup.org/) to provide robust indexing and searching capabilities.

## Table of Contents
+ [Features](#features)
+ [Prerequisites](#prerequisites)
+ [Usage](#usage)
    - [IndexingDocuments](#indexing-documents)
    - [SearchingDocuments](#searching-documents)
    - [DeletingDocuments](#deleting-documents)
+ [ProjectStructure](#project-structure)
+ [Dependencies](#dependencies)

## Features
+ **Multi-format Support**: Indexes and searches PDF, Word, HTML, and image files (e.g., PNG).
+ **Text Extraction**: Utilizes Apache Tika for extracting text from various document formats.
+ **HTML Cleaning**: Uses Jsoup to clean and extract meaningful text from HTML files.
+ **Powerful Search**: Implements Apache Lucene for efficient indexing and searching.
+ **Flexible Deletion**: Provides multiple methods to delete documents from the index based on different criteria.
+ **Extensible**: Easily extendable to support additional document formats or features.

## Prerequisites
+ **Java**: JDK 8 or higher
+ **Maven**: For dependency management and building the project

## Usage
### 1. Prepare Your Data
Create a `data` directory in the project root and place all the documents you want to index inside this directory. Supported formats include:

+ PDF (`.pdf`)
+ Word Documents (`.doc`, `.docx`)
+ HTML (`.html`, `.htm`)
+ Images (`.png`, `.jpg`)

### 2. Configure Index Directory
Specify the directory where the search index will be stored. By default, the example uses an `index` directory in the project root.

### 3. Running the Search Engine
The `SimpleSearchEngine` class contains the main method demonstrating indexing and searching.

#### Example: Indexing Documents
```java
public static void main(String[] args) {
    String indexDir = "index"; // Directory to store the index
    String dataDir = "data";   // Directory containing documents to index
    try {
        SimpleSearchEngine engine = new SimpleSearchEngine(indexDir);
        engine.index(dataDir); // Indexing the documents
        engine.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

#### Example: Searching Documents
```java
public static void main(String[] args) {
    String indexDir = "index"; // Directory where the index is stored
    String queryStr = "your query here"; // Replace with your search query
    try {
        SimpleSearchEngine engine = new SimpleSearchEngine(indexDir);
        engine.search(indexDir, queryStr); // Performing the search
        engine.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

#### Running the Main Method
You can modify the `main` method in the `SimpleSearchEngine` class to perform indexing and searching as needed. After building the project, run the main method using your IDE or via the command line:

```java
mvn exec:java -Dexec.mainClass="com.yourpackage.SimpleSearchEngine"
```

### 4. Deleting Documents
The `SimpleSearchEngine` class provides several methods to delete documents from the index based on different criteria:

+ **Delete by Term**

```java
Term term = new Term("contents", "keyword");
engine.deleteDocuments(term);
engine.writer.commit();
```

+ **Delete by Query**

```java
QueryParser parser = new QueryParser("contents", new StandardAnalyzer());
Query delQuery = parser.parse("some other query");
engine.deleteDocuments(delQuery);
engine.writer.commit();
```

+ **Delete All Documents**

```java
engine.deleteAll();
engine.writer.commit();
```

## Project Structure
```perl
simple-java-search-engine/
│
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── yourpackage/
│                   └── SimpleSearchEngine.java
│
├── data/           # Directory containing documents to index
├── index/          # Directory where the search index is stored
├── pom.xml         # Maven configuration file
└── README.md       # Project documentation
```

## Dependencies
The project uses the following main dependencies managed via Maven:

```xml
<dependencies>
  <!-- Apache Lucene Core -->
  <dependency>
    <groupId>org.apache.lucene</groupId>
    <artifactId>lucene-core</artifactId>
    <version>4.10.4</version>
  </dependency>
  <dependency>
    <groupId>org.apache.lucene</groupId>
    <artifactId>lucene-analyzers-common</artifactId>
    <version>4.10.4</version>
  </dependency>
  <dependency>
    <groupId>org.apache.lucene</groupId>
    <artifactId>lucene-queryparser</artifactId>
    <version>4.10.4</version>
  </dependency>

  <!-- Apache Tika -->
  <dependency>
    <groupId>org.apache.tika</groupId>
    <artifactId>tika-core</artifactId>
    <version>1.28</version>
  </dependency>
  <dependency>
    <groupId>org.apache.tika</groupId>
    <artifactId>tika-parsers</artifactId>
    <version>1.28</version>
  </dependency>

  <!-- Jsoup -->
  <dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.15.3</version>
  </dependency>
</dependencies>
```

Ensure these dependencies are included in your `pom.xml` to successfully build and run the project.

