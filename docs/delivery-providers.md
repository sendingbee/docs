A delivery provider represents a way to send emails. You can have multiple of
them if needed. For each delivery provider you can also specify
daily/weekly/monthly **limits** and set their priority.

By giving each delivery provider a **priority**, SendingBee can prefer
certain providers over others as long as the provider is within its limits.
For example, if the first two providers have priority 100 and the last one
has priority 90, SendingBee will balance between the first two providers as
long as possible and will use the last one only after both of the first two
cannot send anymore.

<p class="centered">
  ![delivery-providers](../_assets/images/delivery-providers.png)
</p>

A delivery provider also has its type. We plan to introduce more types in the
future but as of right now SendingBee integrates with [Amazon Simple Email
Service (AWS SES)](https://aws.amazon.com/ses/). AWS SES is a well known
service used by tens of thousands of businesses around the world.

#### Amazon SES

Amazon SES (AWS SES) is an external product for which you will be charged separately (see
[pricing](https://aws.amazon.com/ses/pricing)). Their pricing is based on
usage which means you will not pay anything if you don't send any emails.
SendingBee uses AWS EC2 instances to send emails and therefore you will be
eligible to
**send 62,000 emails for free every month**. You will then be charged $0.10
for every 1,000 emails after that.

To make this work, you will provide us with very limited keys to your
AWS account. These keys will be created with specific permissions such
that we can only use them to send emails and subscribe to email
notifications. *We will NOT be able to do anything else with your account.*
All keys are stored in encrypted form<sup>1</sup>.

Please continue to [Setup step #1: AWS SES](/delivery-providers/aws-ses).

<sup>1</sup> All keys are encrypted using AES-256-GCM with unique keys and
IVs. Each key is derived using PBKDF2 SHA512 with 100k iterations from
multiple sources with a different level of access.
