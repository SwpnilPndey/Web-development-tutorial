## There are no free lunches in this world 

So, a gasless token transfer is not in wholly gasless. 

It just means :

1. A wants to transfer 10 tokens to B 
2. B doesnot have any ETH to do this transaction (using transferFrom)
3. C has ETH for the transaction 
4. But, C demands 1 extra token as fees to do the transaction 
5. So, effectively, A will transfer 11 tokens to C who will execute the transferFrom function to transfer 10 tokens to B and 1 token to itself 
6. Effectively for A -> B transaction, the transaction is gasless

This is the simple explanation of GASLESS TOKEN TRANSFER. 