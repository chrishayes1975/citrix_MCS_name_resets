# Rectifying issues with Server Names using Citrix Machine Creation Services

This readme will show you how to reset Machine Catalog counts in Powershell

Every so often you'll need to reset the counter for Citrix Machine Creation services in Powershell.

**Current naming conventions for Servers**

* Watford **ftcxa##-wviw-p
* Park Royal **ftcxa##-wvpr-p
* AWS **ftcxa##-wvir-p

What happens is that when you create a new server in a machine catalog it increase what is called the start count by an increment of 1. So if you create a server called ftcxa01-wviw-p the start count moves from 1 to 2. 

Our complexity is that once upon a time we have Citrix Boxes named 01 to 06 and new machine catalogs were created to deploy new images from different delivery controllers. For example we have 4 Machine catalogs for Watford, 2 for Park Royal nd one for AWS.

**Watford**

Watford Machines (current prod, machines from 10-15)
Watford Dev (current dev, machines from 19 onwards)
Watford Test (current Test, machine 09)
Watford New (current test/prod with Windows Server 2012, machines from 01 onwards)

**Park Royal**

Park Royal Machines (current prod, machines from 10-15)
Park Royal (current dev, machines from 19 onwards)

**AWS**

AWS (current test/prod, machines to start from 01)

As you can see above we had multiple machine catalogs. They all use the same naming convention and each Machine Catalog has it's own Pool. So there can be quite a challenge to make sure that the Start Number of each pool is regulated properly otherwise random server names get created and the numbers are all over the place.

So to correct this you need to set each specific pool to have a set start counter number.

We do this in Powershell (launch as administrator)

Type in **asnp Citrix*** . This loads the Citrix Console in Powershell 

Then type in **Get-AccIdentityPool**  

This will list all of the machine pools and all of the Attributes. The ones we are interested in are **PoolName** and **StartCount**.

The **PoolName** links to the Machine Catalog names we create in Citrix. The **StartCount** refers to the number that the machine catalog will start from. 

The Powershell Script you need to run is....

**Set-AcctIdentityPool -IdentityPoolName PoolName -StartCount 1 -NamingScheme TEST####**

Note: poolName refers to the Machine Catalog name and TEST#### refers to the Machine Catalog Naming Scheme

So for example to create a machine in "Waford New" machine catalog and make sure it gets created with 01 (example FTCXA01-WVIW-P) you need to reset the start count to 1.

**Set-AcctIdentityPool -IdentityPoolName "Watford New" -StartCount 1 -NamingScheme FTCXA##-WVIW-P** 

You need the "Machine Pool Name" in quotations if the Machine Catalog contains more than one word.

**Set-AcctIdentityPool -IdentityPoolName AWS -StartCount 1 -NamingScheme FTCXA##-WVIR-P**

If it does contain only one word, there is no need for quotations.

Anyway, after making the **Set-AccIdentityPool** changes above confirm they are working by typing **Get-AccIdentityPool** and checking the relevant fields.

When you then create the new machine in Citrix Studio always make sure that enter the name as either.....

**ftcxa##-wviw-p
ftcxa##-wvpr-p
ftcxa##-wvir-p**

Never enter any numbers in.

Trust in the above and the hashtags



Run **Get-AccIdentityPool**


