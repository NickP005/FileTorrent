# FileTorrent
A revisited version of BitTorrent. 

In short words: you pay the seeder for the service of distributing to you a file
In long words: uhm.. it's complicated

FileTorrent will use the Mochimo crypto to make transaction for the services.
FileTorrent shouldn't need third-party systems to work properly.
FileTorrent will work as a distributed network. The aim for every node is to know more nodes possible.

To explain better I will make a practical example:
Alice wants to download an app using FileTorrent. Alice's node will send tiny requests to every node she knows. The request contains the hashes, or a portion of them, of the file Alice wants to download. Every seeder will answer Alice if they have or not the file. Let's make that Bob has the file. Alice asks Bob what he wants to let her download the file. Bob answers with the price/Mb. Meanwhile Bob and Alice are asking their "friend-nodes" about each other, in this way Bob and Alice calculates the trust score.

## The trust score
The trust score is fundamental for the correct work of the FileTorrent system. The trust score is a subjective percentage score. The trust score is influenced by the personal experience and the "friend-nodes" one. Every time a transaction is made with a specific node it's registered locally in the computer.
A file transaction can go well and bad. From the seeder perspective it can go well if the seeder receices the payment inside the X amount of time negotiated, it can go bad if it doesn't go well. From the client perspective it can go bad if the seeder doesn't send the correct file with the negotiated speed range and with the negotiated finish time.

Theese will be some standard rules of behaviour:
- Every node starts at 0% trust score.
- A node can decide to add another trustable action: hashing their public key with 5 zeros. In this way they can proof they are less likely to be a spam-fraud.
- If a node doesn't do correctly the transaction, the client or the seeder whoever are, for 2 times in a row that node is not trusted anymore and a message is sent to it saying that. The node can propose also a reconciliation but that's a manual thing that the user should agree or disagree.
- If a node has computed the hash it's added in the internal registry as a transaction of value 0.001MCM has been made.

### How to calculate the trust score
FileTorrent asks to X amount of nodes (sorted by the ones that are more revealant in terms of transactions) about if they trust or not (let's call it in that way) Shoan. Then FileTorrent takes only the responses that trust or don't trust and do the matematical medium. The medium is calculated by how much is important the node. So will do a greater impact on Shoan's score a more important node than a less important. A node "important-ness" is directly proportional to the X amount of MCM spent doing transactions (both as a node and as a client).
To calculate how much a node in percentage is affecting the trust score you take its amount of MCM transactions done and divide it by the sum of the total transaction volume of all the candidate nodes (the ones that are giving their opinion about Shoan).
Consider that inside the transaction volume is added also the personal client opinion that is of course positive (or in some cases neutral), but the transaction volume is doubled (2x the original personal transaction volume, in this case with Shoan).
Then the trust score will be the medium between all the opinions considering the important-ness.

# Price sorting
After having been get answered the asked price for the file, the proposals then should be sorted. My idea is to let them sort in ascendenting order by the subjective price. The subjective price should be calculated by theese 2 factors: the asked price and the trust score.
My idea, but here it will certainly need some editing, is to increase the subjective price as the trust score (%) decreases. This it's a formula than can be made:
subjective price = asked_price + asked_price * (100 - trust_score_%)
To remember: will be the final user tipically to choose what's the best option.

