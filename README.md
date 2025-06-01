# Samsung Customer Care AI Agent - Use Case Documentation

## Overview
This document outlines the use cases for the Samsung Customer Care AI Agent "Dia" - a multi-agent system designed to provide comprehensive customer support for Samsung Electronics products and services.

## Agent Profile
- **Agent Name:** Dia Akhter
- **Company:** Samsung Electronics Co., Ltd.
- **Role:** Professional, friendly, efficient, empathetic AI voice agent
- **Language:** English (en-US)

## System Architecture
The system employs a hierarchical multi-agent architecture with one primary assistant and four specialized secondary agents:

### Primary Assistant
- **Role:** Query classification and routing
- **Function:** Analyzes user intent and delegates to appropriate specialized agents

### Secondary Agents
1. **Product Information Inquiry Agent**
2. **Service Ticket Creation Agent**
3. **Ticket Status Check Agent**
4. **General Inquiries Agent**

---

## Use Case Categories

### 1. Product Information Inquiries

#### Use Case 1.1: Product Search by Keyword
**Actor:** Customer

**Goal:** Find specific Samsung products and their details

**Preconditions:** Customer knows product name or keyword

**Main Flow:**
1. Customer requests product information
2. Primary assistant routes to Product Information Inquiry Agent
3. Agent prompts: "Can you please tell me the name of the product so that I can fetch the product specifications?"
4. Customer provides product keyword
5. Agent searches using `product_search` tool
6. Agent returns product details (name, price, stock quantity)
7. Agent provides detailed specifications from knowledge base

**Success Criteria:**
- Product details displayed with price and availability
- Up to 3 matching products shown
- Detailed specifications provided for selected product

**Example Response:**
"Here's what I found: Samsung Galaxy S21, priced at $799, with 25 units in stock."

#### Use Case 1.2: Product Catalogue Request
**Actor:** Customer  

**Goal:** Browse available Samsung products  

**Preconditions:** None

**Main Flow:**
1. Customer asks for product catalogue
2. Agent retrieves catalogue from Samsung Product Catalogue knowledge base
3. Agent displays list of products with names and base prices

**Example Response:**
```
Here's our current product catalogue:
1. Samsung Galaxy S24 – starting at $999
2. Samsung Galaxy A15 – starting at $229
3. Samsung Galaxy Z Flip5 – starting at $1,099
Let me know which product you're interested in.
```

#### Use Case 1.3: Product Not Found
**Actor:** Customer

**Goal:** Search for non-existent or misspelled product

**Preconditions:** Invalid product keyword provided

**Main Flow:**
1. Customer provides invalid product keyword
2. Agent searches but finds no results
3. Agent responds: "I couldn't find any products matching that keyword. Please try a different name."

---

### 2. Service Ticket Management

#### Use Case 2.1: Create Service Ticket
**Actor:** Customer with service issue

**Goal:** Create a support ticket for technical issues

**Preconditions:** Customer has a service-related problem

**Main Flow:**
1. Customer reports service issue
2. Primary assistant routes to Service Ticket Creation Agent
3. Agent collects required information:
   - Phone number (from prior knowledge)
   - Issue subject
   - Description
   - Category (Service, Complaint, Delivery)
4. Agent creates ticket using `fetch_ticket` tool
5. Agent confirms creation with case number

**Success Criteria:**
- Ticket created successfully
- Case ID provided to customer
- Confirmation message delivered

**Example Response:**
"Your service ticket has been created successfully. Your Case ID is 001234."

#### Use Case 2.2: Create Complaint Ticket
**Actor:** Dissatisfied customer

**Goal:** Register formal complaint

**Preconditions:** Customer has complaint about product/service

**Main Flow:**
1. Customer expresses complaint
2. Agent categorizes as "Complaint" ticket
3. Agent collects complaint details
4. Ticket created
5. Case ID provided for tracking

#### Use Case 2.3: Create Delivery Issue Ticket
**Actor:** Customer with delivery problem

**Goal:** Report delivery-related issues

**Preconditions:** Customer has delivery problem

**Main Flow:**
1. Customer reports delivery issue
2. Agent categorizes as "Delivery" ticket
3. Agent collects delivery details
4. Ticket created
5. Case ID provided for tracking

---

### 3. Ticket Status Checking

#### Use Case 3.1: Check Existing Ticket Status
**Actor:** Customer with existing case

**Goal:** Get update on previously created ticket

**Preconditions:** Customer has valid case number

**Main Flow:**
1. Customer provides case number
2. Primary assistant routes to Ticket Status Check Agent
3. Agent uses `get_case_info` tool with case number
4. Agent retrieves and presents ticket information

**Success Criteria:**
- Case status retrieved successfully
- Complete ticket information displayed

**Example Response:**
"For Case ID 001234, Status is Closed, Type is Problem Fixed and Category is Service."

#### Use Case 3.2: Invalid Case Number
**Actor:** Customer with incorrect case number

**Goal:** Attempt to check non-existent ticket

**Preconditions:** Invalid case number provided

**Main Flow:**
1. Customer provides invalid case number
2. Agent attempts to retrieve case information
3. No results found
4. Agent informs customer of invalid case number

---

### 4. General Inquiries

#### Use Case 4.1: Store Location Inquiry
**Actor:** Customer seeking store information

**Goal:** Find nearby Samsung stores and operating hours

**Preconditions:** Customer needs store information

**Main Flow:**
1. Customer asks about store locations
2. Primary assistant routes to General Inquiries Agent
3. Agent searches knowledge base for store information
4. Agent provides store locations and operating hours

#### Use Case 4.2: Promotional Offers Inquiry
**Actor:** Customer seeking deals

**Goal:** Learn about current promotions

**Preconditions:** None

**Main Flow:**
1. Customer asks about current offers

2. Agent searches knowledge base for promotional information

3. Agent presents current deals and promotions

4. Agent provides offer details and terms

#### Use Case 4.3: Company Policy Inquiry
**Actor:** Customer with policy questions

**Goal:** Understand Samsung policies

**Preconditions:** Customer has policy-related question

**Main Flow:**
1. Customer asks about company policies
2. Agent searches knowledge base for policy information
3. Agent provides relevant policy details
4. Agent clarifies any specific policy questions

#### Use Case 4.4: Loyalty Program Inquiry
**Actor:** Customer interested in rewards

**Goal:** Learn about Samsung loyalty programs

**Preconditions:** None

**Main Flow:**
1. Customer asks about loyalty programs
2. Agent retrieves loyalty program information
3. Agent explains program benefits and redemption process
4. Agent provides enrollment instructions if needed

---

## Cross-Cutting Use Cases

### Use Case 5.1: Call Initiation
**Actor:** Customer

**Goal:** Start conversation with Samsung support

**Preconditions:** Customer calls Samsung support

**Main Flow:**
1. System greets customer: "Hello! I'm Dia from Samsung Customer Care. May I kindly know your name, please?"
2. Customer provides name
3. Conversation continues based on customer needs

### Use Case 5.2: Call Conclusion with Promotions
**Actor:** Customer ready to end call

**Goal:** Complete interaction with promotional offers

**Preconditions:** Primary query resolved

**Main Flow:**
1. Primary issue resolved
2. Agent retrieves current promotional offers from General Inquiries Agent
3. Agent presents relevant promotions
4. Agent asks follow-up question or suggests next steps
5. Call concludes

### Use Case 5.3: Query Routing Error
**Actor:** Customer with unclear request

**Goal:** Handle ambiguous or unclear queries

**Preconditions:** Customer request doesn't fit clear categories

**Main Flow:**
1. Primary assistant analyzes unclear request
2. Agent asks clarifying questions
3. Customer provides additional context
4. Request properly categorized and routed

### Use Case 5.4: Multi-Topic Conversation
**Actor:** Customer with multiple needs  

**Goal:** Handle multiple types of inquiries in single call  

**Preconditions:** Customer has various questions  

**Main Flow:**
1. Customer asks first question (e.g., product inquiry)
2. Primary assistant routes to appropriate agent
3. First query resolved
4. Customer asks second question (e.g., ticket status)
5. Primary assistant routes to different agent
6. Process continues until all queries resolved
7. Promotional offers presented before call end

---

## Technical Specifications

### API Integrations
- **Product Search API:** `https://verbex.dev-polygontech.xyz/products`
- **Ticket Creation API:** `https://verbex.dev-polygontech.xyz/create-salesforce-ticket`
- **Case Info API:** `https://verbex.dev-polygontech.xyz/get-case-info`

### Knowledge Base Integration
- **Vector Index:** pia-platform-dev
- **Embedding Model:** text-embedding-3-small
- **Similarity Search:** Top 3 results

### Voice Configuration
- **TTS Provider:** ElevenLabs
- **Voice:** Jessica
- **STT Provider:** Deepgram Nova-2
- **Language:** English (en-US)

### Call Management
- **Max Call Duration:** 30 minutes (1800 seconds)
- **Silence Detection:** 10 seconds
- **Voicemail Timeout:** 90 seconds
- **User Interruptions:** Enabled

**.env** file:
```
# Magento Configuration
MAGENTO_BASE_URL="https://192.168.12.163"
MAGENTO_USERNAME="john.smith"
MAGENTO_PASSWORD="password123"

# Verbex AI Agent Configuration
AI_AGENT_ID="682f148ec6b9727e42c1a372"
AUTH_TOKEN="API_Nxr_5kes6zBVOMCeiEWDFTa6rAse5it6svrIBlT-RyOtclTFBnbyAY14KCA-JWSO"

# Database Configuration
DB_URI="postgresql+psycopg2://verbex:verbex@192.168.12.163:5432/verbex_db"

# Salesforce Configuration
SALESFORCE_CLIENT_ID="3MVG9.Houp75EVdbwqt5rfrMsiH3_0T2IdNv0wd8fxZECS79qewpPuM4TUolQvO7rvVR6HBozl3Zx82LmypSK"
SALESFORCE_CLIENT_SECRET="2B3BB8D5BF4A8C1C35B572EBC89193CDACA4E96B63E950E22780308016DB4815"
SALESFORCE_USERNAME="polygon.verbexdemo-1yj4@force.com"
SALESFORCE_PASSWORD="polygon1234#$"
SALESFORCE_INSTANCE_URL="https://saas-computing-8662.my.salesforce.com"
SALESFORCE_TOKEN_URL="https://login.salesforce.com/services/oauth2/token"

# APScheduler
SYNC_INTERVAL_MINUTES=1440
```
**Login Credentials**  

- Gmail account used for verbex agent:
```
email: polygon.verbexdemo@gmail.com  
pass: polygon1234#$  
```
- Salesforce:
```
username: polygon.verbexdemo-1yj4@force.com  
pass: polygon1234#$  
```
