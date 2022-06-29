Dear Recruiting Team,

Thank you for this opportunity to create this module. It was challenging, educational and a pleasure to complete!

I thought it might be interesting to give you some insights into my thought process and my challenges as I worked through this excersice. 

## Thought Process
A blank canvas or in this case a blank module can be one of the most challenging obstacles to overcome. Given the opportunity to create a module topic I'm passionate about, I wanted to do someting around security and hoped to include Datadog into the module

After several days of contemplation, I came up with three scenarios:

1. Create and deploy a crypto miner in AWS and use the DataDog Agent to detect and alert on it.
2. Illustrate the Impossible Time Travel scenario, where a user logs into AWS from Los Angeles and then from Madrid 15 minutes later. Again, using  DataDog's security tools to detect and alert around this.
3. Illustrate and explain one of the most common cyber attacks, the SQL Injection.

## Challenges
As I began to explore scenario one, I quicly realized that not only would this be difficult to keep to 15 minutes, but also given my current resources it would be extremely difficult to build out in a module that could be easily reproduced for the learner. Deploying a crypto miner and wallet customized to the learner would likely take 15 minutes on it's own. Though, this would be a fun project!

The second scenario seemed more plausible. I bult my AWS EC2 environment out and got my Datadog agent running successfully. However getting SIEM up and running proved more challenging. Spinning up all the necessary AWS services with CloudFormation and CloudTrail would again take more time and resources than I had and would also be difficult to keep to under 15 minutes for a module. Also, including a VPN application to replicate the locations would be challenging

So I settled on SQL injection. It seemed staight forward and repeatable.

One challenge with my chosen topic was that the OWASP Juice shop itself contains Type Script. It took a bit of digging to figure out the Type Script requirements  for the Datadog Agent.

## Outcome
Overall I'm pleased with how the module turned out. It was/is difficult to determine if it would actually only take 15 minutes to compete. Also, given a series of starts, stops and restarts, it took longer than expected. 

I ran through the module myself on a fresh laptop and it worked for me as expected. 

# My Datadog user experience
I'm pleased with the results I achieved with the agent blocking the attack and all the details it captured. One aspect that was odd was that often the RUM App wouldn't report any data incoming. Does it require a certain amount of data before it engages?

I loved the free trial and even had an amazing experience with Datadog support! 

Thank you for this opportunity! I hope you enjoy my module. If selected for hire I would be excited to flesh this module out more for actual use by Datadog customers.

Sincerely,
Steve Davidson