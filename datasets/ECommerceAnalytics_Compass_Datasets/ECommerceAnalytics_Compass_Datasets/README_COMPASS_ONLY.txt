ECOMMERCE ANALYTICS — MONGODB COMPASS ONLY DATASET PACK

Included synthetic datasets:
- customers.json: 10,000 documents
- products.json: 5,000 documents
- orders.json: 100,000 documents
- reviews.json: 20,000 documents
- inventory_logs.json: 10,000 documents
- query_logs.json: 4 documents
- optimization_recommendations.json: 4 documents

IMPORTANT:
1. These are synthetic practice records, not real customer data.
2. Import each file into the matching collection in the ECommerceAnalytics database.
3. Importing into an existing collection adds documents; it does not automatically remove old sample records. If you want clean counts, delete existing documents in each collection before importing, or create a fresh database.
4. For each file: open the collection -> Documents -> Add Data -> Import JSON or CSV File -> select the .json file -> choose JSON -> Import.
5. Each file is a JSON array of documents. Dates use MongoDB Extended JSON ($date) format.
6. Import one file at a time. Wait for completion before importing the next file. The 100,000-order file is the largest and may take a while.
7. After import, use the Aggregations tab for reports and Indexes tab to create indexes.

Recommended indexes (create manually in Compass -> collection -> Indexes -> Create Index):
orders:
  {"customer_id": 1}
  {"customer_id": 1, "order_date": -1}
  {"product_id": 1, "status": 1}
  {"status": 1, "order_date": -1}
  {"payment_method": 1, "status": 1}
reviews:
  {"product_id": 1, "rating": -1}
  {"customer_id": 1}
inventory_logs:
  {"product_id": 1, "timestamp": -1}
  {"movement_type": 1, "timestamp": -1}
customers:
  {"city": 1, "membership_tier": 1}
products:
  {"category": 1, "price": -1}

Suggested first aggregation on orders:
Stage 1:
{"$group":{"_id":null,"total_sales":{"$sum":"$total_amount"},"order_count":{"$sum":1},"average_order_value":{"$avg":"$total_amount"}}}
Then click Run. The values shown depend on this synthetic dataset.
