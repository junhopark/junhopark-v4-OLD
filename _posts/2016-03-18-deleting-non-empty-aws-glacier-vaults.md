---
layout: posts
---

I had a couple of AWS Glacier vaults that I had been meaning to permanently delete for awhile.  When I tried deleting them via the AWS dashboard, I got the following error message:

    Vault not empty or recently written to: arn:aws:glacier:us-east-1:[Some sort of ID]:vaults/[Glacier Vault Name]

After contacting AWS support as well as doing some Googling, I discovered that I was going to have to first delete all of the archives in my vaults and that the only way to delete the archives was to use the AWS Command Line Interface (CLI).  I think it's silly that I can't just delete non-empty vaults from the dashboard, but whatever.

So I installed the AWS CLI by following the steps on http://docs.aws.amazon.com/cli/latest/userguide/installing.html and took a stab at trying to delete the archives.  Well, I quickly learned that AWS CLI is not very intuitive.  Actually, for what I was trying to do, it was **absolutely horrible**.

I tried to delete my vaults using the *delete-vault* command.  That did not work, of course, because my vaults weren't empty.

I then discovered [on this page](http://docs.aws.amazon.com/cli/latest/reference/glacier/index.html) that there is a *delete-archive* command.  Here's the problem, though:  One of my vaults contained **272,475** archives.  In addition, one of the required arguments when calling the *delete-archive* command is the *Archive ID* parameter and the way that I had to go about obtaining this information was maddening.  I needed to call the *initiate-job* command to initiate a *inventory-retrieval* job and then call the *get-job-output* command to retrieve information that contains the Archive IDs, which outputs it to an unformatted JSON file, which contains all of the Archive IDs.  Yep, maddening.  I was unable to find an easier way to obtain this information.

Well, after thinking to myself "there's got to be a better way to do this", I came across [glacier-vault-remove](https://github.com/leeroybrun/glacier-vault-remove).

It's a Python script that "will remove all archives contained inside the vault, and then remove the vault itself".

PERFECT.

I kicked off the script and it ran for about THREE FULL DAYS.  After the script exited, I logged back into the AWS dashboard and to my horror, I saw that my 2 vaults were still there.  However, this time around, I was able to successfully delete the 2 vaults.  FINALLY!  glacier-vault-remove had successfully removed all of the archives and simply failed to remove the vaults.

The lesson to be learned here is that if you've got Glacier vaults you'd like to permanently delete - use glacier-vault-remove.
