# Sweet Crumbs Orders – AI Bakery Assistant

This project is a chat-based order assistant built for **Sweet Crumbs Home Bakery**. It helps customers place cake and cupcake orders through a conversation instead of filling out a form.

I built this using LangChain, Pydantic and Google Sheets, so the assistant can understand customer messages, check bakery timings, calculate prices and save orders.

## 

-  `is_open(day)` checks whether the bakery is open on the requested day.
-  `get_price(item, qty)` gets the price based on the menu and quantity.
-  `log_order(...)` validates the order details and saves them to Google Sheets.

## Handling customer messages

Customers don't always provide details in a proper format. They might say something like:

> hey can i get a choclate cake for Sriharsha this sunday, make sure it is eggless

Using Pydantic and `with_structured_output(Order)`, the assistant converts the message into structured data:

- Name: Sriharsha
- Item: Chocolate cake
- Quantity: 1
- Date: This Sunday
- Eggless: Yes

The order is validated before being processed.

## Google Sheets Integration

The assistant connects to Google Sheets using `gspread` and stores order details in a sheet called **Sweet Crumbs Orders**.

If the sheet doesn't exist, the notebook can create it automatically. This makes it easier to keep track of customer orders without manually entering every detail.

## Experiments

### 1. Structured Output Test

I tested the assistant with five different customer messages, including informal and incomplete-looking sentences, to see how well it could extract order details. It successfully converted them into structured data.

### 2. The "Break It" Experiment

I renamed the `get_price` tool to `tool1` and replaced its description with *"Mangled tool that does stuff."*

Even with the unclear name and description, the model was able to identify the tool when asked something like *"How much are 5 cupcakes?"* and pass the required parameters.

It was an interesting way to test how the model handles poorly described tools.

### 3. Multi-Turn Trace Analysis

I also checked how the assistant handled a conversation involving multiple steps.

In the trace I analysed:
- **3 model generations**
- **2 tool calls** – `is_open` and `log_order`

This helped me understand how the model decides when to call tools and how the steps are executed during a conversation.
