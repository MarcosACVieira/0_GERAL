# VoC – 5 ticket questions (customer side only)

Input per ticket: the customer's own messages (text) + facts from the table, given to the reader as context:
session_types, n_sessions, n_customer_msgs, n_pictures, csr_spoke, wait_seconds, duration_seconds, last_sender.
Answer only from what the customer wrote; the facts help to judge, never replace the text.
One answer per question, always one of the listed codes.

## q1_resolution – was the problem solved, from the customer's point of view?
- `solved`      the customer thanks, confirms it worked, or says it is fine now
- `partial`     accepts with a reservation ("ok, but…", "fine, I'll wait")
- `unsolved`    complains at the end, insists, says it was not solved or that they will come back
- `no_signal`   the customer leaves without saying anything that shows the outcome

## q2_csat – estimated satisfaction at the end
- `dissatisfied` (≈ CSAT 1–2)  anger, frustration, sarcasm, complaint about the service at the end
- `neutral`      (≈ CSAT 3)    no clear emotion either way
- `satisfied`    (≈ CSAT 4–5)  thanks, relief, praise

## q3_effort – how hard was it for the customer (CES)?
- `low`     explained once and that was it
- `medium`  had to add details or information
- `high`    repeated the same thing, complained about waiting or bots, sent proof several times,
            "??" follow-ups, or came back in another session (n_sessions > 1 counts as a hint)

## q4_risk – most severe loss signal written by the customer
- `none`
- `leave_app`   says they will stop using / delete the app or stop driving
- `competitor`  names or hints at a competitor (Uber, inDrive, Cabify…)
- `external`    Procon, PROFECO, court, lawyer, police report, press, social media

## q5_request – what the customer wants from DiDi (not what happened)
- `money`        refund, reversal, payment, compensation
- `explanation`  understand a charge, a rule, a block, a decision
- `fix`          change something in the account, registration, trip or app
- `report`       punish or report the driver / passenger
- `other`

## Sampling and use
- 150 tickets per CR from the launch sample (3,000 per segment, 6,000 total), same hash order as the cause labels.
- One model per question per segment (not per CR): TF-IDF + MiniLM + the table facts, logistic regression.
- Trained once from the launch labels; no automatic retraining. Daily: the 50 sampled tickets per CR are also
  answered, only to measure accuracy and raise an alert.
- Reliability check before trusting a question: a second, independent reader answers 300 tickets;
  agreement below 75% -> simplify that question's options.
