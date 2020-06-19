# Design Mint

## Question

If there are many components in the system, do I need to define all the APIs between every two component?



Mint.com is a free, web-based personal financial management service, that allows its users to integrate with financial accounts to automatically extract their data, and manage their personal budget.

Design a system like Mint.

{% embed url="https://www.pramp.com/challenge/4E4NW7NjbnHQEx1Axo73" %}

## Feature Scope

* Connect Mint account with my financial accounts
* Pull my financial data
  * when I log in
  * periodically to give me financial suggestions

## API Design

```text
syncUserData(userId, back?)
```

userId: GUID of user

bank?: If not provided, sync all my bank info; otherwise, just sync the info of this bank.

```text
getSuggestions(userId)
```

Given userId, give a list of suggestions. Example

```text
[
    { bank: "Chase", suggestions: ["Pay loan on time"] },
    { bank: "Bank of America", suggestions: ["Use less than 10% of credit card limit"] }
]
```

## High-level Design

### Basic Setup

![](../.gitbook/assets/image%20%2852%29.png)

### Scaling

#### DB

As we get more and more users, the throughput of the system might not be the first issue, the DB size could be.

We can horizontally scale the DBs.

We can use Consistent Hashing to map the userId to a specific DB instance. When we add or remove DB instance, we just migrate a fraction of the user data to other DB instances. 

![](../.gitbook/assets/image%20%2853%29.png)

#### Application Server

If the user base continues growing, a single application server can't handle all the requests and we need to scale it.

We can add a load balancer to distribute the load across multiple application servers.

![](../.gitbook/assets/image%20%2843%29.png)

#### Web Server

The last thing we hit scaling issue might be the web server since they are only hosting static contents.

We can introduce CDN to improve the availability and performance of the static content retrieval.

We can also scale the single web server to a cluster and add load balaner to distribute the requests.

![](../.gitbook/assets/image%20%2844%29.png)

## Database Design

### Objects

* User: userId, authToken
* UserBank: userId, bank, other user data specific to the bank

Since the UserBank data might be different across different bank. One solution is that we use different tables for different banks. But even if we do that, a specific bank might change their schema as well. So since the data schema might not be stable, I'd prefer to use NoSQL DB.

### Relationships

The relationship between User and UserBank table is connected using userId.

## Back-of-the-envelope calculation

Assume we have 1M DAU, each of them logs in to the portal once per day, then the average QPS is 1M / 24 / 60 / 60 = 11.6 Q/s. If each request taks 100KB, then it's 1.2MB/s.

Assume we have 50M users in total and each user has 3 banks on average, each of them require 2MB information. Then the total storage is 50M \* 3 \* 2MB = 30TB.

