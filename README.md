# Problem

### (from Balance Internet)

We need to send lots of data to Magento via the web API, particularly for products and stock which have thousands of updates each day. 

Some requests are also very slow, like updating an attribute that has hundreds or thousands of options, and this creates timeouts. 

Magento produces deadlocks on various tables at any more than 1 concurrent request for product updates. The higher number of requests, the more deadlocks are created. This creates a lot of failed requests which must be retried continuously before the update is saved by Magento. 

Below shows an example response from Magento when a deadlock is created:

POST http://example.org/rest/default/V1/products/` resulted in a `400 Bad Request` response:\n{\"message\":\"Unable to save product\"}

PUT (update) product requests create deadlocks at approximately 1/10th of the rate for POST (insert) requests. 

Most commonly the deadlock is a gap lock against one of the EAV tables for product which is required for the database to be replication-safe. 

Optimising the existing interfaces is ideal as this doesn’t require any change in logic for existing API clients. 

--

Enterprise Support Ticket #03208263
Error "Unable to save product" under high concurrency using REST API - Deadlock
