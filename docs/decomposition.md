### Step 1 

"Create an inventory application with search and stock filters."
3 decisions that an AI needs to make before implementation: 

It needs to decide how data is stored and how to retrieve that information
-> fo example: Will data be stored in a data class or in a dictionary?, What data will be stored?
It needs to decide the structure of the functions: 
-for example: Will filtering and retrieval work in the same function or two seperate ones? 
The names of functions and classes and what they mean
-> for example: What is a a Product and what information is stored in it? 
It needs to decide the presentation of the application 
-> Will the CLI be interactive in speech - can the user ask follow up questions? Or interactive in with a list of options? What information will be presentated?


### Step 2
Actors and their Goals: 
Inventory Employee: 
-View active products 
-Filter by stock staus
-Be able to search products by name or SKU

Business Rules: 
-Only active products are shown
-stock status comes from stock quantity 
-products can be searched by name or SKU

Open Question: 
-is the name search case sensitive? 
-is full SKU necessary? 
-what happens in case of empty input or output? 

One process 
1.Employee enters a search term 
2.System processes the term to make it readable
3.System matches it with what we have in the system 
4.System retreives the item using filter 
5.System displays the item and its status 

View
See the status of the product

Controller
Coordinate the search process

Business Logic
Normalize the term and determine stock status 

Model 
Retreive info from database (CSV file, mongoDB, or API)



### Step 3 
You are helping decompose an application into implementation-ready issue
files.

## Input

## Functional description

The situation

A small retailer currently manages its inventory in a spreadsheet. Employees lose time scrolling through rows and sometimes use outdated stock information.

The retailer wants a product overview in which an inventory employee can:

see active products;
search by product name or SKU;
filter products by stock status;
open the details of one product;
see when the stock information was last updated.
Every product has:

id
sku
name
description
price
stock quantity
active status
last updated date and time

Use the following stock statuses:

Out of stock:  quantity = 0
Low stock:     quantity = 1 through 5
In stock:      quantity > 5

The first version is read-only. Employees do not add products or adjust stock yet.

## Actors and goals
Inventory Employee: 
-View active products 
-Filter by stock staus
-Be able to search products by name or SKU

Business Rules: 
-Only active products are shown
-stock status comes from stock quantity 
-products can be searched by name or SKU

Open Question: 
-is the name search case sensitive? 
-is full SKU necessary? 
-what happens in case of empty input? 

## Business rules and expected results

Business Rules: 
-Only active products are shown
-stock status comes from stock quantity 
-products can be searched by name or SKU

Open Question: 
-is the name search case sensitive? 
-is full SKU necessary? 
-what happens in case of empty input? 

## Process flow

1.Employee enters a search term 
2.System processes the term to make it readable
3.System matches it with what we have in the system 
4.System retreives the item using filter 
5.System displays the item and its status 

## Responsibilities
View
See the status of the product

Controller
Coordinate the search process

Business Logic
Normalize the term and determine stock status 

Model 
Retreive info from database (CSV file, mongoDB, or API)


## Available skills

- `../inventory-engineering-skills/SKILLS.md`
- `../inventory-engineering-skills/skills/app-configuration.md`
- `../inventory-engineering-skills/skills/file-structure.md`
- `../inventory-engineering-skills/skills/function-definitions.md`
- `../inventory-engineering-skills/skills/validation.md`

## Project constraints

- use Build a command-line inventory search or a small report using pandas and a CSV file.

Focus on:

input schema and validation;
pure search, filter and stock-status transformations;
separation between file access and processing;
readable terminal or report output;
pytest.

- keep business rules independent from UI and data access
- generate tests for every business rule
- generate one User Story with acceptance criteria for every actor goal
- keep every issue small enough for one branch and pull request
- do not generate implementation code yet

## Generate

1. A concise requirement summary.
2. User stories ordered by dependency.
3. A functional breakdown for each user story.
4. Separate `ISSUE-n.md` files.

Every issue must use this structure:

# ISSUE-n.md

## Title

## User Story

## Functions

## Required Skills

## Expected Output

## Validation

## Rules

- Keep each issue small enough for one branch and one pull request.
- Give each issue exactly one main user story.
- List the functions the implementation should expose or use.
- Reference `.skills/SKILLS.md` in every issue.
- Add relevant topic-specific skills.
- Define reviewable output and validation criteria.
- Split unrelated behavior into separate issues.
- Do not generate implementation code yet.




