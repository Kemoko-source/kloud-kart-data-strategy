# Recommendation & Roadmap

## Executive Recommendation: What We Build and Why


### What we will build:
1.  **A MySQL Read Replica:** We will mirror our live database onto a second, pre-approved server. 

2.  **In-Database SQL Transformations:** We will clean and shape our data using standard SQL directly on that second server.

3.  **A Single BI Tool:** We will connect a free, open-source dashboard tool (like Metabase or Superset) directly to the replica. 

4.  **A Compliance Pipeline:** An automated script to delete customer data across our systems to satisfy the Data Protection Commission (DPC).

### Rough Cost: 
The infrastructure cost is negligible—the price of one extra standard cloud server (roughly $100–$200/month) and zero expensive software licenses. The true cost is the salaries of the two engineers we hire to build and maintain it. 

### Why this fits Kloud Kart, not Amazon:
*   **It stops the bleeding immediately:** Moving reporting to a Read Replica instantly cures the Monday site crashes. Analytical queries will never touch the live shop again.

*   **It is staffable:** Two engineers can easily maintain a MySQL replica and a BI tool. They cannot maintain a multi-layer cloud lakehouse while also keeping the core business online. 

*   **It solves the real problem:** Our problem isn't that our database is too small; it's that Nana and Finance disagree on math. We need to invest in *people* agreeing on definitions (Semantic Layer), not expensive software.

---

## The Hiring Plan: First Two Roles

### Hire #1: Data Engineer
*   **Why them first?** We have to stop the website from crashing and fix our Act 843 compliance issue before we do anything else. We need a plumber before we need an interior decorator. 

*   **First 90 Days:** Stand up the MySQL Read Replica, decouple Nana’s Monday reports from the live production database, set up the hosting for our new BI dashboard, and build the automated Act 843 deletion pipeline to get the DPC off our backs. 

### Hire #2: Data Analyst
*   **Why them second?** A data analyst builds business logic and dashboards, which they cannot do safely until the Read Replica is built. 

*   **First 90 Days:** Sit down with Nana and Finance to write a single, unified definition of "Revenue." Audit the old spreadsheet formulas, translate them into version-controlled SQL models on the new server, and build the official company dashboards.

---

## 12-Month Roadmap (Quarterly Outcomes)

### QUARTER 1: Stop the Bleeding
*   **Who is better off:** Nana Adjei (Operations) & Customers

*   **What changes:** Heavy analytical reporting no longer touches the live shop.

*   **How it is verified:** On the first Monday in April, Nana opens her weekly report at 08:00. The website response time does not spike, and the checkout page remains perfectly fast for shoppers. 

### QUARTER 2: The "Single Source of Truth"
*   **Who is better off:** Finance and Operations

*   **What changes:** We stop using unmanaged Excel spreadsheets to calculate company revenue. We use one centralized system with an agreed-upon math formula.

*   **How it is verified:** By June 30th, the Head of Finance and Nana both bring the exact same revenue number to the board meeting, pulled from the exact same dashboard link. 

### QUARTER 3: Compliance & Privacy Lockdown
*   **Who is better off:** Legal Counsel & The Board

*   **What changes:** We completely lock down how data is copied, eliminating unmanaged CSV files on laptops, and automate customer deletion requests to comply with Act 843.

*   **How it is verified:** By September 30th, Legal submits a test "customer deletion request." Within 5 working days, they receive an automated log proving that customer’s data was wiped from every analytical system and backup we own.

### QUARTER 4: Scaling for the Nigeria Pilot
*   **Who is better off:** The Executive Board & Expansion Team

*   **What changes:** The data platform scales to handle the Nigeria pilot, ensuring cross-border data is cleanly separated for reporting without mixing up currencies or metrics. 

*   **How it is verified:** By December 31st, the board can open the executive dashboard and view side-by-side performance of Ghana vs. Nigeria, easily filtering out one country to see the other, with zero manual data cleaning required.