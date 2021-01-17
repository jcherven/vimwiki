# Week 02 Day 01

# introducing dbeaver

an interactive interface for the database. manages db connections, allows editing and runnin queries in an editor.

sql developer is not good, avoid it. dbeaver has many more features

for training, we'll use a single db named `postgres`. superuser `postgres` for simplifying use locally.

dbeaver provides the ability to let you see your DB as automatic ER diagrams, or as table grids.

you should also have an AWS account. sign up for a free aws account. we will be leveraging RDS (at this point). two others will be used later on.

## AWS

AWS can be used if you don't want to run a local instance. it's also just good to get a bit of experience with AWS.
### RDS

name: `rev-post-database`

db instance size: free tier

creds: username `postgres`

db instance size: `burstable classes`

connectivity:
public access: `yes`
security group:
  - create new
  - vpc security group name: `myRevSecurity`
  - default port (5432)

daabase authentication: `password authentication`

everything else default

...then create the database.

on the RDS dashboard, not the endpoint and port. verify.

Edit inbound rules:
  - add a rule for your public IP address.
  - or use `0.0.0.0/0` `::/0` to allow global access. unsafe, but whatever
  - save rules

in dbeaver, you can add the RDS instance as a new connection with the endpoint and port.
