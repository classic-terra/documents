Background


Proposal 11889 (https://station.terraclassic.community/proposal/columbus-5/11889) has been the first step towards a pay-per-job structure. However, it lacks many details for a practicable implementation plan. Furthermore, it doesn’t provide guidelines and costs for reviewing and deploying a job and does not account for the potential running costs of teams. This proposal aims to expand and change some details of proposal 11889 for a practicable implementation of the pay-per-job structure while offering necessary flexibility.

## I. Scope of pay-per-job

1. An accepted job format must have a clear start and a measurable definition of what is done. A job bidder must provide a defined roadmap, a specific timeline, a designated team, and the required resources for successful execution.
2. A job format without a clear start or without a measurable definition of what is done is considered out of scope (e.g. infrastructure tasks, recurring tasks). The proposer will need to explain why not adhering to the pay-per-job format. Proposing this kind of job does not violate the pay-per-job plan.
3. A bundle of jobs is permissible, given adequate reasons justifying the need for bundling. This bundle may include both types of job formats mentioned above, provided that the entire bundle has a clear start and a measurable definition of done.

## II. Proposed implementation

* The most recent approved pay-per-job plan will be maintained on classic-terra GitHub for implementation. All future changes must be approved by governance.
* Job listings can be proposed through text proposals or direct proposals on classic-terra GitHub by using the appropriate issue template. If proposed via text proposal, upon passing, the program manager will put up that job on classic-terra Github. The details of the job listing application form will be in section “II. Job listing application form”.
* After the bidding process, the bidder can then proceed with a spend proposal detailing the implementation plan at their own discretion. Terms of a spend proposal are defined in section “V. Disbursement terms”.
* After the spend proposal is approved, the bidder may proceed with the work and can submit several pull requests. Failure to implement within the proposed time frame will require the bidder to explain the delay to the community. If the bidder party fails to convince the community, the community has the right to demand the return of the remaining funds to the community pool via a binding text proposal.
* Reviewing pull requests is the function of either the Terra Classic core party reviewers or the Terra Classic community. The Terra Classic core party reviewer will review and either approve or reject the pull request, providing a public report on the results if rejected. The reviewing process by Terra Classic core party reviewer may include an extension of the deadline for the bidder. Final approval of pull requests are either done by the core party reviewer or superseded by a governance vote (see section VIII. Reviewing terms).
* Once the pull requests are merged, the Terra Classic core party will plan for its mainnet deployment.
* After the job is concluded, the program manager will record the results in the public job entry.

#### Notice:
* The community and validators are responsible for ensuring no more than one spend proposal for the same job is passed should multiple teams bid on a job. The bidders are not responsible for issues arising from multiple passed spend proposals for the same job.
* If there are no new significant commits to bidder pull requests for more than one month, other contributors will deem the works abandoned and available for free use.
* Both Terra Classic core party and bidders liabilities for contributions are defined by the Apache 2.0 license

## III. Job listing application form
A job listing application form is intended to inform the community of the issues or features requested. Therefore, it must contain the following information:

* Proposer’s Contact Information:
  * Twitter, Discord, and TG for future contact and discussion.
* Description of Issues/Improvements.
  * What specific problem are you encountering?
  * How does it affect your experience?
  * What potential improvements can be suggested?
* Examples
  * Please illustrate your points with examples or scenarios. This could significantly enhance understanding.
  * Please provide sufficient pictures or documents as you see fit.
  * Expected definition of done
  * How can resolving this job help you and the community?
  * How do you define “done” for this job? A job listing needs to follow the terms outlined in “I. Scope of pay-per-job”

## IV. Bidding process
The bidding process helps the bidder to understand the steps for efficient bidding.

* The bidder can reach out directly on the corresponding GitHub job posts or through governance approved Commonwealth
* The bidder will include all relevant information in their bid application. This includes
  * Executive summary
  * Team members (or Company name) and their Social Media names (or Company social media)
  * GitHub profile(s) of all team members (or Company github) for reference to earlier jobs and work experience
  * KYC certificate (if existing)
  * A specific roadmap for the job stages
  * A specific timeline for the job implementation
  * Payment conditions (see section V. Disbursement terms)
  * Further information that might help the community and validators to judge the suitability for this specific job
* Bidders must post their bid application on the approved Commonwealth platform, including links to the related GitHub job posts.
* After 7 days, the bidder can propose their bid application to on - chain governance through either a text or spend proposal. A spend proposal must adhere to “V. Disbursement terms”.
* If the bid proposal is rejected, the bidder can make necessary changes and resubmit the proposal without waiting an additional 7 days on the approved Commonwealth.

#### Bidding terms:
* It is valid to be a bidder and proposer for the same job.
* If a job is granted to one bidding party via governance, the remaining bidders should drop their bid application.

## V. Disbursement terms
A bidder may expect disbursement terms as follows:

* Payment is disbursed following governance approval for each proposed payment stage. The payment schedule is up to their best standards and practices.
* The bidder may add upfront payment (also referred to as setup cost and/or retainer fee) to the bid application to account for expenses or team cost.
* If a job takes more than 4 weeks, the bidder may request intermediate payment(s).
* It is the bidder’s responsibility to justify upfront and intermediate payments towards governance.
* Payment terms in either text or spend proposal must not deviate from the payment terms in the bid application.

## VI. Validator cooperation

The validator cooperation is voluntary. This pay-per-job plan is designed to assist validators in making informed decisions with input from trusted community members.


Validators must ensure no more than one spend proposal for the same job is passed should multiple teams bid on a job. The bidders are not responsible for issues arising from multiple passed spend proposals for the same job.

## VII. Associated pay - per - job program management roles

1. The program manager role description:
* Collecting, reviewing, and putting up job posts
* Connect and provide relevant information to job proposers, validators, bidders, and pay-per-job program members
* Aid bidders in connecting to relevant parties and required resources
* The program manager is not a gatekeeper with no veto privileges on job proposals

2. The Terra Classic core party reviewer tasks per project:
* Talk with bidders and job proposers
* Setup required tests to ensure compatibility and successful upgrades
* Provide a report outline the reasons for rejecting a pull request
* Plan mainnet upgrades for approved pull requests
* Any mainnet issues resulting from the approved pull request will be handled accordingly to section VIII. Reviewing terms.

## VIII. Reviewing terms
Reviewing terms provide protection to bidders, reviewers, and the community. It provides a framework to define responsibilities in the event of mainnet issues.


Reviewing rights:
* The Terra Classic core party reviewer consisting of engineers with write access to the source code of Terra Classic core
* The Terra Classic community consisting of delegators and validators

1. General Terms
* The Terra Classic core party will merge the bidder’s works upon approval from either the Terra Classic core party reviewer or the Terra Classic community through governance proposals
* The Terra Classic core party will aid with code deployment for testnet and mainnet per requests from the bidder

2. The Terra Classic core party reviewer terms
* The Terra Classic core party reviewer will share debugging and resolving responsibility with bidders on pull requests that are approved by the reviewer
* The Terra Classic core party reviewer will collaborate with bidders to debug and resolve testnet and mainnet issues if debugging responsibility is shared
* The Terra Classic core party reviewer reserves the right to deny approval responsibility on a job with a public post explaining the reason. In this scenario, the reviewer will not assume any responsibility for testnet and mainnet issues arising from the bidder’s works
* If a bidder does not include a core reviewer into the application, the Terra Classic core party reviewer can submit a request for review proposal on an ongoing work to governance. If approved, the bidder is obligated to adhere to the outlined review process
* The Terra Classic core party reviewer liabilities for contributions are defined by the Apache 2.0 license

3. The bidder party terms
* The bidder holds the responsibility for resolving any issues stemming from their code after it is deployed on the testnet and mainnet. If the bidder cannot or does not undertake necessary fixes in a reasonable amount of time, it is then upon the Terra Classic community to either ensure the bidder fulfills this responsibility or to identify and engage other contributors, who may be compensated or voluntary, to address necessary fixes
* The bidder is encouraged to contact and include a Terra Classic core party reviewer in their bid application along with associated costs outlined in section IX. Associated pay - per - job suggested costs
* If a core reviewer is included in their bid application or approved by governance, online meetings are required during the whole reviewing process, depending on the scope of work to review, e.g. for discussing the contributed code and plan for the work deployment on mainnet or testnet
* The bidder liabilities for contributions are defined by the Apache 2.0 license

## IX. Associated pay - per - job suggested costs
1. Fixed costs:
* The program manager: voluntary


This amount is a suggestion only. An amount agreed on by the nominated program manager has to be included in the nomination proposal (see section IX. nominations)

2. Flexible costs:
* The Terra Classic core party reviewer per approved project: 1000$ + 15% of proposal value/project. This cost is included into a bid proposal as an upfront cost. If a Terra Classic core party reviewer decides not to take responsibility for reviewing and approving a contribution, or no core reviewer is included in the bid proposal by the bidder, nor approved by governance (see section VIII. Reviewing terms), no payment is due for the review job.

3. Total costs per quarter
* The program manager: voluntary
* The cost for the Terra Classic core party reviewer is an additional item included in the upfront payment of an approved project.

## X. Nominations
Proposed individuals for the mentioned roles are as follows

1. Program manager: To be nominated and approved through a community proposal


The pay-per-job plan will be managed voluntarily by the cooperation between TCC and JL1TF until a program manager is nominated and approved through a community proposal. All nominations/positions as well as adjustments to the plan are subjected to governance.