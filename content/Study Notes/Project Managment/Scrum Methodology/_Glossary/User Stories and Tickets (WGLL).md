---
tags:
  - Scrum
  - UserStories
---
A ticket describing new functionality typically contains:

-   A User Story (Authored by PM/PO in feature/product Brief)
-   Acceptance Criteria (Authored by Tech Lead or Design)
-   Tests (Authored by Tech Lead)
-   Any Security Considerations. (Authored by Tech Lead)


A well drafted ticket can be read by anyone on the SCRUM team. From it they will understand: 

-   why a piece of functionality is being developed
-   the purpose of the functionality    
-   what needs to happen for the functionality to be realized in the product    
-   how to test that the functionality exists when deployed.    
-   how to test for software failures
-   any compliance or security tests and/or requirements that need to be completed, checked, or signed off before deployment.
  

NOTE: A user story is the simplest possible requirement and describes only one piece of functionality.

A ticket should have a INVEST way of being constructed:

[Independent](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Independent)
The story should be self-contained, in a way that there is no inherent dependency on another story.

[Negotiable](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Negotiable)
Stories are not explicit contracts and should leave space for discussion.

[Valuable](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Valuable)
A story must deliver value to the stakeholders.

[Estimable](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Estimable)
You must always be able to estimate the size of a story.

[Small](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Small)
Stories should not be so big as to become impossible to plan/task/prioritize within a level of accuracy.

[Testable](https://en.wikipedia.org/wiki/INVEST_(mnemonic)#Testable)
The story or its related description must provide the necessary information to make test development possible.

## Ideal Ticket Structure

### User Story focused on achieving benefit.

“As a <mark style="background: #BBFABBA6;">_User Role_</mark>  I want <mark style="background: #BBFABBA6;">_some goal_</mark> so that <mark style="background: #BBFABBA6;">_receive some benefit from the functionality_</mark>”

### Acceptance Criteria Scenarios

For each user scenario:

-   Given    
-   When
-   Then
   
### Tests

Describe each test scenario:
-   Precondition, actions and expected results 
-   Steps (optional detail in the ticket, but need to be detailed out in actual test case)
-   Links to Testrail test cases before “Done”

### Analytics
Describe what’s needed for analytics in order to measure the efficacy of this feature:

-   Events logging
-   Analytics DB data requirements
-   Analytics data pipelines
-   Out-of-the-box reports
-   Monitoring and alerts

### Security
Describe areas of security concerns

-   Security areas to assess
-   Chat channel security - website or messaging channel handling the user session
-   User authentication - only right user can access right data at right time
-   Cross-tenant security - data cannot leak from one tenant to another
-   PII handling - PIIs are redacted or securely stored temporarily
-   Messaging security - messages are not exposed during and after transmission
-   Banking API security - Banking APIs are properly secured
-   Data storage - sensitive information is securely stored both in transit and at rest
-   Proper expiration of tokens and caches
-   Proper secret handling 

-   (Architecture) If this follows existing security pattern, describe the reference patterns it falls into - can be multiple

-   Message encryption in SDK (transmission and browser cache)
-   Data stored in encrypted DB at rest
-   Manage secrets in Vault and injection method  
-   All HTTP traffic in TLS, and all internal traffic in mTLS
-   All secrets are managed in Vault
-   Proper handling of user tokens in application
-   PII redaction pipelines and periodical redaction reviews
-   Static Content security in S3 and CDNs
-   K8s hosting and approved data centers for data residency
-   No sensitive information in logging stack

-   If this introduces new security concerns, task to perform security review

  
## Rearchitecting an existing user story to What Good Looks Like

As a user, when I ask for my direct deposit info or the routing number for an account, I want the bot to return a list of my checking and savings accounts with the corresponding direct deposit/routing number details.

  
**Acceptance Criteria**

<Screenshots/animations of what you designed> 

-   As an authenticated user when I ask for my direct deposit info OR for the routing number on my accounts 
-   I am provided with a gallery of all my checking and savings accounts
-   With each gallery card having an account name, account number (even if it is just the last four digits of account number) and routing number
-   If I ask for direct deposit information or routing number for a specific account I will receive information only for that account
-   If I ask for direct deposit information or routing number for an account that isn’t recognized by the bot I will receive a response asking me to check the account name and try again or to ask in a more generic way to receive the information for all accounts
-   If I ask for the direct deposit information or routing number for all my accounts but there are no applicable accounts found I will receive a response letting them know this.
-   Add test scenarios that are specific for Truist use cases

### The above user story is not using the proper format. We could change it to:

<mark style="background: #FFB8EBA6;">As a</mark> bank customer, <mark style="background: #FFB8EBA6;">I want</mark> to ask the bot for my direct deposit information and have it return a list of my checking and savings accounts with the corresponding direct deposit/routing numbers <mark style="background: #FFB8EBA6;">so that I can</mark> have funds deposited directly into my accounts from my employer/vendor/government agency.

However, both the original and reformatted stories are highly explicit and do not give space for discussion. <mark style="background: #FF5582A6;">This story is not Negotiable</mark>. And the user would never say that. 

<mark style="background: #FFF3A3A6;">The story needs to focus on the benefit and not be prescriptive. This provides flexibility. We can negotiate how this (the scope) can be achieved - given time, and resources.  </mark>

### What Good Looks Like:  User Story

<mark style="background: #FFB8EBA6;">As a</mark> bank customer, <mark style="background: #FFB8EBA6;">I want to be able to</mark> quickly get the direct deposit information for all of my checking and savings accounts <mark style="background: #FFB8EBA6;">so that I can</mark> <mark style="background: #ADCCFFA6;">what exactly will the user do with the numbers</mark> in order to have funds deposited directly into my accounts from my employer/vendor/government agency.

Note: the above does not describe the solution.

### WGLL: AC using Given/When/Then (This is how we solve the story)

**Scenario A:** Authenticated Bank Customer Asks for routing number for specific account by its name.  

Given that I’m in a role of Authenticated Bank Customer
When I ask the bot for the routing information for a specific account
Then the bot shows me that bank account with the corresponding routing number.

**Scenario B:** Authenticated Bank Customer Asks for routing number for all my accounts

Given that I’m in a role of Authenticated Bank Customer
When I ask the bot for the routing information for my accounts or ALL my accounts
Then the bot shows me a list of all my bank accounts with the corresponding routing number.  

**Scenario C:** Authenticated Bank Customer Asks for routing number for specific account by wrong name

Given that I’m in a role of Authenticated Bank Customer
When I ask the bot for the routing information for a specific account that does not exist in my records
Then the bot responds “that it can not find an account under that name. Please check the spelling or enter in the account number.”

**Scenario D:** Authenticated Bank Customer Asks for routing number for all my accounts but no accounts exist with associated routing numbers.

Given that I’m in a role of Authenticated Bank Customer
When I ask the bot for the routing information for all my accounts AND none of the accounts have a corresponding routing number 
Then the bot responds “Your present accounts do not support routing numbers.”

Variant 1: *Unauthenticated* Bank Customer Asks 
Then the bot responds “You must login to view your account information.”

Variant 2: Authenticated Bank Customer Asks for *Direct Deposit Number* not routing number
Then the bot responds with Scenarios A, B, C, D

Note: Variants must apply to all scenarios, otherwise, write a new scenario  
**