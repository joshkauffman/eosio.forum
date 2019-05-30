<h1 class="contract">clnproposal</h1>

---
spec_version: 0.1.1
title: Clean Proposal
summary: Clear the RAM being consumed to hold voting and proposal data for {{ proposal_name }} once expired
icon: NEED TO ADD
---

This action is used to clear the RAM being used to store all information related to
{{ proposal_name }} in {{ max_count }} rows. All associated votes must be cleared before {{ proposal_name }}
can be cleared from the RAM of the `proposer`.

This action can be called by any user, requiring no authorization.

This action can only be called 72 hours after `expires_at` of {{ proposal_name }} has been reached.
`expires_at` is set at the moment that {{ proposal_name }} is created, and can
only be updated by the `proposer`. This will allow time to compute a tally of all
associated votes before it can be cleared.

The user who calls `clnproposal` will pay the CPU and NET bandwidth required
to process the action. They will need to specify `max_count` to ensure that the
action can be processed within a single block's maximum allowable limits.

<h1 class="contract">expire</h1>

---
spec_version: 0.1.1
title: Expire
summary: Change the `expires_at` value of {{ proposal_name }} to the current time
icon: NEED TO ADD
---

## Description

`expire` can only be called by the `proposer` of {{ proposal_name }}.

`expire` is used to modify the value of `expires_at` to the current time at which the action is called. Once `expire` has been called, no more `vote` actions will be accepted for {{ proposal_name }}. {{ proposal_name }} can be cleared from RAM 72 hours after `proposer` has called the `expire` action by using the `clnproposal` action.

<h1 class="contract">post</h1>

---
spec_version: 0.1.1
title: Post
summary: Create a post with the unqiue identifier {{ post_uuid }}
icon: NEED TO ADD
---

`post` is used to create a post that can either be a parent or
be a response to a parent post. They are threaded together using their
unique identifier {{ post_uuid }}.

<h1 class="contract">propose</h1>

---
spec_version: 0.1.1
title: Propose
summary: Create the proposal {{ proposal_name }}
icon: NEED TO ADD
---

`propose` creates a message on-chain with the intention of receiving
votes from any community members who wish to cast a `vote`.

Each proposal shall be identified with a unique `proposal_name`.

An expiry will be defined in `expires_at`, with {{ expires_at }}
being no later than 6 months in the future.

{{ proposer }} must pay for the RAM to store {{ proposal_name }}, which
will be returned to them once `clnproposal` has been called.

<h1 class="contract">status</h1>

---
spec_version: 0.1.1
title: Status
summary: Set a status of {{ content }} for account {{ account }}
icon: NEED TO ADD
---

`status` is used to record a status for the associated {{ account }}.
If the {{ content }} is empty, the action will remove a previous status.
Otherwise, it will add a status entry for the {{ account }} using the
{{ content }} received.

<h1 class="contract">unpost</h1>

---
spec_version: 0.1.1
title: Unpost
summary: Request for removal of {{ post_uuid }} by {{ poster }}
icon: NEED TO ADD
---

The intent of the `unpost` action is to suggest that a previously posted message (through the `post` action), as referred by {{ post_uuid }}, be removed by the different front-ends reading this contract's transaction flow.

I, {{ poster }}, understand that this action will not remove the message from circulation, as it will be imprinted in the blockchain.  I also understand that some front-ends might not remove the message, and even highlight the fact that a message was intended to be removed, potentially attracting attention on an undesired message.

<h1 class="contract">unvote</h1>

---
spec_version: 0.1.1
title: Unvote
summary: Remove the previous vote action of {{ voter }} on proposal {{ proposal_name }}
icon: NEED TO ADD
---

`unvote` allows {{ voter }} to remove the vote that they have previously
cast on {{ proposal_name }}.

`unvote` will not function during the 72 hour period after
{{ proposal_name }} has expired.

The RAM that was used to store the vote shall be freed-up immediately
after `unvote` has been called by {{ voter }}.

If {{ voter }} has a proxy set and the proxy has a vote set on {{ proposal_name }}, then
the vote weight of {{ voter }} will return under their proxy's control. If this is unwanted,
{{ voter }} should elect to cast an abstain vote.

<h1 class="contract">vote</h1>

---
spec_version: 0.1.1
title: Vote
summary: Cast a vote of {{ vote }} with the vote weight of {{ voter }} for proposal {{ proposal_name }}
icon: NEED TO ADD
---

I, {{ voter }}, am casting a vote of {{ vote }} on {{ proposal_name }}. To change my vote, I may call another `vote` action, with only the most recent `vote` of {{ vote }} being the `vote` which I, {{ voter }}, intend to be considered as valid. I acknowledge that using the `unvote` action after placing a `vote` will render my previous `vote` of {{ vote }} null and void. 

If I, {{ voter }}, have a proxy registered for my on-chain voting, my own `vote` of {{ vote }} shall take precedence over my proxy's vote. My stake weight shall be deducted from their voting power and cast as my own. 

If I, {{ voter }}, am not the beneficial owner of these tokens, I stipulate I have proof that I’ve been authorized to vote these tokens by their beneficial owner(s).

If I, {{ voter }}, am registered as a proxy and am casting votes on behalf of other users of the blockchain, I acknowledge that I am doing so on their behalf and that they may at any time withdraw their stake weight from my voting power by casting their own vote or removing my account as their proxy.

I, {{ voter }}, stipulate I have not and will not accept anything of value in exchange for this `vote`, on penalty of confiscation of these tokens, and other penalties.
