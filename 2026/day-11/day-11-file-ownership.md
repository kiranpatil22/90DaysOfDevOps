Task 1: Verify Ownership (5 Marks)

Run ls -l in your home directory.

Identify:

Owner column

Group column

Write the format of the output:
-rw-r--r-- 1 owner group size date filename

Question:
What is the difference between owner and group?

Task 2: Basic Ownership Change (10 Marks)

Create a file:
touch devops-test.txt

Check current ownership:
ls -l devops-test.txt

Change owner to tokyo.

Change owner to berlin.

Verify changes.

Command syntax:
sudo chown username filename

Task 3: Group Management (10 Marks)

Create group:
sudo groupadd heist-team

Create file:
touch team-notes.txt

Change group of file to heist-team.

Verify using:
ls -l team-notes.txt

Command syntax:
sudo chgrp groupname filename

Task 4: Owner + Group Together (10 Marks)

Create file:
touch project-config.yaml

Change:
Owner → professor
Group → heist-team

(Use single command)

Verify.

Syntax:
sudo chown owner:group filename

Task 5: Recursive Ownership (15 Marks)

Create directory structure:

mkdir -p heist-project/vault
mkdir -p heist-project/plans

Create files:

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf

Create group:
sudo groupadd planners

Change ownership of entire heist-project directory:

Owner → professor
Group → planners

(Use recursive option)

Verify using:
ls -lR heist-project

Task 6: Final Challenge (20 Marks)

Create directory:
mkdir bank-heist

Create files inside:

touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt

Set ownership:

access-codes.txt → owner: tokyo, group: vault-team
blueprints.pdf → owner: berlin, group: tech-team
escape-plan.txt → owner: nairobi, group: vault-team

Verify:
ls -lR bank-heist

