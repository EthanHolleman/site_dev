---
title: "Getting started with UC Davis High Performance Computing: A grad student's perspective"
date: 2021-04-01
tags: ['guides', 'programming', 'blogs']
draft: true
---

## Who is this for?

This guide is intended for graduate student researchers at UC Davis who need to gain access to UC Davis cluster computing resources for their research. The information is
current as of the day of posting.

The goal is to cover the logistics of actually obtaining your login credentials
(username and ssh key), not how to actually use those credentials to interact
with computing resources (covered in the [CSE wiki here](https://wiki.cse.ucdavis.edu/support/general/security/ssh) and [here](hhttps://wiki.cse.ucdavis.edu/farm_guide?s[]=create&s[]=account))

While the CSE wiki has some good information, I found it difficult to
navigate and find the links I needed and found myself taking actions to create
an account that go beyond the short 
[How to Get an Account](https://wiki.cse.ucdavis.edu/support/faq/how_to_get_an_account?s[]=create&s[]=account) guide. This was mostly due to human elements, as for best
results you will need to involve your PI, and possibly other administrators.

## Getting Access

### Step 1: Find out where you are working

Figure out where your lab does their compute. You can see a full list of
cluster's at the 
[UC Davis High Performance Computing site](https://www.hpc.ucdavis.edu/clusters).

For life science labs this is likely either the FARM, the Genome Center cluster
(also shown as LSSC0), or Crick. While I have so far only used LSSC0, Crick and FARM LSSC0 seems to be the most distinct and uses their own registration system.

### Step 2: Register

Tell your PI you are registering for an account, as usually they will need
to approve your access.


#### Non-genome center registration

Create your ssh private-public key pair that you will use to login, follow
[this guide](https://wiki.cse.ucdavis.edu/support/general/security/ssh). 

Register your public key using the [account request form](https://wiki.cse.ucdavis.edu/cgi-bin/index2.pl). This will send your request into the ether and not provide
you with any feedback. 

I have found that it is helpful to email at the same time with the
subject along the lines of 
**[Cluster Name] account request for grad student in PI lab** to 
hpc-help@ucdavis.edu with some additional info about what you are trying to do
and cc your PI. This seems to get a human working on your approval faster as
the HPC support team, at least in my experience, has been very helpful and fast
when contacted directly.

#### Genome center registration

If you are going to be working on the Genome Center cluster you should
register for an account using their [registration page here](https://computing.genomecenter.ucdavis.edu/registration/register/).

After your PI approves your registration you should get an email from 
accounts@genomecenter.ucdavis.edu telling you that your account has been
approved and a companion email that will allow you to set your password. 

### Step 3: Make sure everything is working

Once you have been approved for access test your login right away to make sure
everything is working well. 











