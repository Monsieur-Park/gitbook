---
description: your first Graph
---

# Your First Graph

* You can create a new project by clicking on the “New” button on the screen’s top left.

![create graph](/pic/01-4-1.jpg)

 * After installation, click “New Graph” under My Project section,
 then “create a Local Graph”. Write down the name of the graph, and the password.
![local graph](/pic/01-4-2.jpg)

![password graph](/pic/01-4-3.jpg)

* Run the database, clicking the “play” sign.

![play graph](/pic/01-4-4.jpg)

Now open the neo4j browser with the new graph you created.
A bar at the top will appear and you’ll type queries there

![browse graph](/pic/01-4-6.png)

# Connecting to a Remote DBMS from Neo4j Desktop

To configure your Neo4j Desktop to connect to your GrapheneDB database instance, open the Project tab inside Neo4j Desktop, and select **Add Graph** → **Connect to remote Graph.**

1. Add Graph.

![add graph](/pic/e948898-addgraph.png)

2. Connect to remote Graph.

![Connect graph](/pic/0071de1-connectremotegraph.png)


3. Supply Database Name and Connect (Bolt) URL.

![Supply Database](/pic/4554a83-nameandbolt.png)

4. You can find the Bolt URL to your database by navigating to the connection tab of your admin panel inside GrapheneDB.

5. To connect your database user, please select username / password.

![password](/pic/a1ae3a6-username.png)

6. You must select the checkbox to Use encrypted connection, otherwise you will not be able to connect to the remote GDB database.

![checkbox](/pic/ef33e6c-encryption.png)

# Browser

**The Neo4j browser** is a graphical user interface (GUI) that can be run through a browser.

The Neo4j Browser is the easiest way to access Neo4j database.
It requires a port and a bolt connection to access the database.

The browser can be used for adding data, running queries, creating relationships, and more.
It also provides an easy way to visualise the data in the database.

1. The default port for Neo4j browser is : http://localhost:7474/browser/
2. The default bolt protocol for Neo4j browser is : bolt://localhost:7687

Before we fall deep into modelling, let’s mention and learn basics how to use database UI.
Launch Browser will redirect you to screen below.

![browse graph](/pic/neo4j_browser.png)

* Blue — Database & Connection information
* Yellow — Nodes, Relationships and Properties (nothing here yet)
* Red — Query input box (click ESC to expand/collapse)
* Green — Execute query button (Clean and Add to Favorites actions nearby)

# Cypher

* **CYPHER** is a flexible language, you can create nodes, relationships and even both together at the same time.
* the main idea to understand is a concept of **Graph Pattern Matching.**
* Let’s say your data is about **people and organisations.**
  - People are one kind of ‘node’ and Organisations are another kind.
  - They can be connected through a specific relationship.
  - Like someone has worked for a company, someone is the chairman of the company, or a company is the parent of another company.

* Your First Query:
  - Create nodes then relationships.
  - Create a node with the following syntax:
  **CREATE ( x: LABEL { ATTRIBUTE_NAME: ATTRIBUTE_VALUE })**

Where
  **x: is a variable name of the node**, you could call it whatever.
  **It’s useful when you reuse it for instance to plot the node at the end of the query using RETURN x.**
  **LABEL: is the label of the node. In our case we’ll have 2 labels: Org and Person**

For Instance:

  ``CREATE (p: Org { Name: "Max Planck" })
  ``

![company](/pic/company.png)


Hit enter and you’ll get a confirmation (or an error) that the node was created.
In my case, it worked, as mentioned by **Added 1 label, created 1 node…**

By the way, by running the above query we’ve implicitly created a label called Org.
Let’s create a person who is the employ of this organisation and associate him to the organisation.

  ``CREATE (p: Person { Name: "Yohan Park" })``

Then

``MATCH (p:Person),(o:Org)
  WHERE p.Name = "Yohan Park" AND o.Name = "Max Planck"
  CREATE (p)-[r:works]->(o)
RETURN p,r,o
``

![relationship](/pic/relationship.png)


Adding the **RETURN** at the end of the query will plot the newly created relationship.
 Note that Neo4j has a color coding that differentiates labels automatically.

Now we kind of understand how **CYPHER** works: either you create something new and start with **CREATE**, or
you try to find existing things in the graph and you start with **MATCH**.
Nodes are in brackets (), relationships in square brackets [], attributes in curly brackets {}

# Bloom

**Bloom** is a graph data visualisation and exploration tool. Rather than using Cypher to interrogate your data, Bloom allows you to use near-natural language to ask questions instead.

Bloom is accessible via Neo4j Desktop. With this new version of Bloom, you will be able to explore data on a local Neo4j instance, as well as customising your perspective for your needs.

You can customise Bloom by setting up the perspective.
There are a number of things you can do to customise the perspective to your specific use-case:

* Colour-code labels and relationships — As well as choosing colours for your node labels,
you can now also select colours based on relationship types.

* Use **icons** to help visually describe nodes rapidly —
Select the most appropriate image for your node categories from an extensive library of icons.


![bloom_install](/pic/bloom_install.png)

* Pattern-based search

These patterns should help quickly identify how to ask questions in the form of Bloom phrases.
The following patterns we’ll cover are:

- Specific path:

We use this pattern when we want to retrieve all of the information from a specific start point.
For example we may be asking a question from an anchor point.

![bloom](/pic/bloom.png)


- Shortest path:

This pattern is very useful for starting to understand the shortest path between two nodes.

- Paths between nodes:

This pattern is very useful for revealing potentially different paths of a certain pattern between set start an end points.
