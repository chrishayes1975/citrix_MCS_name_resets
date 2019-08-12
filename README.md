# citrix_MCS_name_resets

This readme will show you how to reset Machine Catalog counts in Powershell

Every so often you'll need to reset the counter for Citrix Machine Creation services in Powershell.

Current naming conventions for Servers

* Watford ftcxa##-wviw-p
* Park Royal ftcxa##-wvpr-p
* AWS ftcxa##-wvir-p

What happens is that when you create a new server in a machine catalog it increase what is called the start count by an increment of 1. So if you create a server called ftcxa01-wviw-p the start count moves from 1 to 2. 

Our complexity is that once upon a time we have Citrix Boxes named 01 to 06 and new machine catalogs were created to deploy new images from different delivery controllers. For example we have 4 Machine catalogs for Watford, 2 for Park Royal nd one for AWS.

Watford

Watford Machines (current prod, machines from 10-15)
Watford Dev (current dev, machines from 19 onwards)
Watford Test (current Test, machine 09)
Watford New (current test/prod with Windows Server 2012, machines from 01 onwards)

Park Royal

Park Royal Machines (current prod, machines from 10-15)
Park Royal (current dev, machines from 19 onwards)

AWS

AWS (current test/prod, machines to start from 01)

As you can see above we had multiple machine catalogs. They all use the same naming convention and each Machine Catalog has it's own Pool. So there can be quite a challenge to 


