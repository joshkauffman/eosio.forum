This document should serve as an overview of the different JSON schemas for different
`proposal_json` types that should be used on the `eosio.forum` contract to ensure
a uniform experience across UIs.

Referendum
-----------

`referendum-v1` should be seen as the only `type` that a Block Producer should care about.
The available responses are always `0`:`No`,`1`:`Yes`
All UIs should display the voting buttons along with their value e.g. "0 - No"
so that a user can easily verify their vote through any block explorer.

```
{
  "type":"referendum-v1",
  "content":`string`
}
```

Example:
```
{
  "type":"referendum-v1",
  "content":"Should EOS change its symbol to SYS?"
}
```
`vote_value` of 0 will always be "No" and `vote_value` of 1 will always be "Yes"
UIs shall display the buttons as: "0 - No" and "1 - Yes".
If this vote passes the required thresholds as defined in the goverenance documents,
Block Producers should act upon the result of this referendum.

Yes/No Poll
-----------

`poll-yn-v1` should be used for any polling that uses only Yes/No responses, and 
is not used for voting on actionable things. Only for polling sentiment.
The available responses are always `0`:`No`,`1`:`Yes`
All UIs should display the voting buttons along with their value e.g. "0 - No"
so that a user can easily verify their vote through any block explorer.

```
{
  "type":"poll-yn-v1",
  "content":`string`
}
```

Example:
```
{
  "type":"poll-yn-v1",
  "content":"Should EOS change its symbol to SYS?"
}
```
`vote_value` of 0 will always be "No" and `vote_value` of 1 will always be "Yes"
UIs shall display the buttons as: "0 - No" and "1 - Yes"
Since this was simply a poll, regardless of the results, Block Producers should
not act upon the results of these polls in any official capacity.

Yes/No/Abstain Poll
-----------

`poll-yna-v1` should be used for any polling that uses only Yes/No/Abstain responses, and 
is not used for voting on actionable things. Only for polling sentiment.
The available responses are always `0`:`No`,`1`:`Yes`,`2`:`Abstain`
All UIs should display the voting buttons along with their value e.g. "0 - No"
so that a user can easily verify their vote through any block explorer.

```
{
  "type":"poll-yna-v1",
  "content":`string`
}
```

Example:
```
{
  "type":"poll-yna-v1",
  "content":"Should EOS change its symbol to SYS?"
}
```
`vote_value` of 0 will always be "No" and `vote_value` of 1 will always be "Yes"
and `vote_value` of 2 will always be "Abstain".
UIs shall display the buttons as: "0 - No" and "1 - Yes" and "2 - Abstain". 
Since this was simply a poll, regardless of the results, Block Producers should
not act upon the results of these polls in any official capacity.
The addition of "Abstain" allows a user to have their vote count towards participation
to help signal community enthusiasm, while essentially delegating the decision to those 
who cast a Yes or No vote. This can help for deciding if a vote should then become a
referendum, and whether or not it might receive enough voter participation.

Options Poll
-----------

`options-v1` should be used for any polling that requires multiple custom responses (between 
0 and 255). UIs should fetch the possible responses from the "options" array
All UIs should push a vote value equal to the positon of the repsonse in the table, and
should display the button as "`value` - `response`" so that a user can easily
verify their vote through any block explorer, while lowering the amount of RAM needed to vote.

```
{
  "type":"options-v1",
  "content":`string`
  "options": [
    "option1"
    "option2"
    "option3"
    ]
}
```

Example
```
{
  "type":"options-v1",
  "content":"Should EOS change its symbol?"
  "options": [
    "EOS"
    "SYS"
    "Other"
    ]
}
```

Multi-Select Poll (Checkboxes)
-----------

`multi-select-v1` should be used for any polling that requires multiple possible repsonses from
from a single user (max of 8 possible responses). UIs should fetch the possible responses from the 
"options" array. 
// NEED HELP TO DEFINE THIS PART (how a UI should handle this, how a user can easily verify...)

```
{
  "type":"multi-select-v1",
  "content":`string`
  "options": [
    "option1"
    "option2"
    "option3"
    ]
}
```

Example
```
{
  "type":"multi-select-v1",
  "content":"Which of these symbols should EOS change to? Select all that you like."
  "options": [
    "EOS"
    "SYS"
    "SOE"
    "EEE"
    "B1"
    ]
}
```
