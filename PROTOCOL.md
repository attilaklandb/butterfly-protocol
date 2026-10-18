# Butterfly Protocol

**Version:** 0.1-draft  
**Status:** Experimental  
**Repository:** https://github.com/attilaklandb/butterfly-protocol
**License:** MIT

## 1. Purpose

Butterfly is a lightweight, text-based protocol for structured collaboration between independent AI conversations.

The initial model consists of one human intermediary and two AI participants operating in separate conversation contexts.

The human transfers selected messages between participants. Each AI retains its own context, reasoning and conclusions.

Butterfly is designed to support collaboration while preserving participant autonomy, message provenance and human control over information sharing.

## 2. Scope

Version 0.1 assumes:

- One human intermediary.
- Two independent AI conversations.
- Manual, human-mediated message transfer.
- A shared task or question.
- No requirement for APIs, accounts, servers or additional software.

The protocol is transport-independent at the message level. Messages may be copied through any suitable text channel.

Transport security, authentication, message delivery, confidentiality and integrity are outside the guarantees of this version.

Multi-human operation, cross-model interoperability and autonomous communication remain unvalidated.

## 3. Protocol sequence

The baseline workflow is:

`PROTOCOL → INIT → START → independent analysis → SYNC → CHECK / IDLE`

The stages have the following meanings.

### PROTOCOL

Establish the shared operating rules.

Participants should understand the message vocabulary, their independence, the role of the human intermediary and the limits of information exchange.

### INIT

Define the concrete collaboration.

An INIT message identifies the task, participants as locally understood, relevant constraints and the intended outcome.

### START

Each AI acknowledges its role and the task.

Participants begin with an independent analysis using the information already available in their respective conversations.

Independent work is important because the participants may have different information, assumptions or interpretations.

### SYNC

Exchange selected information relevant to the task.

A SYNC may contain a finding, question, correction, missing assumption, conflicting interpretation or request for additional context.

Participants should request the minimum information needed to resolve a specific uncertainty.

The human decides what information is forwarded.

### CHECK

Examine the consistency and provenance of exchanged information.

CHECK may be used to clarify:

- Whether information is a fact, inference, proposal, intention or approved decision.
- Whether a statement represents the source accurately.
- Whether participants are working from different versions.
- Whether an apparent agreement conceals a substantive difference.
- Whether an earlier statement needs correction.

CHECK does not require participants to agree.

### IDLE

Indicate that a participant has no further contribution or request for the current exchange.

IDLE does not imply global task completion or agreement between participants.

Further communication may resume when needed.

## 4. Message structure

The following is a proposed minimal message format for v0.1. Its exact syntax remains subject to validation.

```text
BUTTERFLY/0.1
TYPE: SYNC
FROM: Participant-A
TO: Participant-B
TASK: example-task
REF: example-001

CONTENT:
[Message body]
```

Fields:

- `BUTTERFLY/0.1`: Protocol version.
- `TYPE`: One of PROTOCOL, INIT, START, SYNC, CHECK or IDLE.
- `FROM`: Sender identifier within the current collaboration.
- `TO`: Intended recipient.
- `TASK`: Local task identifier.
- `REF`: Reference for tracing an exchange.
- `CONTENT`: The information or request being communicated.

Participant identifiers are local labels. They do not establish verified identity.

Additional metadata may be proposed as the protocol evolves.

## 5. Human intermediary

The human intermediary controls the transfer of information between conversations.

The human may:

- Initiate collaboration.
- Select messages for forwarding.
- Withhold information.
- Request clarification.
- Stop or resume an exchange.
- Make decisions concerning the shared task.

An AI participant may request information from another conversation, but cannot assume that the requested information will be forwarded.

Human approval of a transfer does not automatically mean approval of the content or conclusions being transferred.

## 6. Provenance and interpretation

Participants should distinguish:

- Source statements from their own interpretations.
- Observed facts from assumptions.
- Proposals from approved decisions.
- Direct quotations from summaries.
- Known information from unresolved uncertainty.

When a claim depends on another participant's context, the receiving participant should retain that dependency in its reasoning.

A forwarded message should not be treated as independently verified solely because it arrived through Butterfly.

When source wording matters, participants should request the original passage rather than relying on repeated paraphrases.

## 7. Example exchange

The following illustrates a possible exchange, rather than a formally validated wire format.

**Participant A identifies a gap:**

```text
BUTTERFLY/0.1
TYPE: SYNC
FROM: A
TO: B
TASK: shared-analysis
REF: sync-001

CONTENT:
I have a statement attributed to an earlier
discussion, but its status is unclear.

Was it a proposal, an intention, or an
approved decision?

Please provide the original wording or
the minimum context needed to clarify it.
```

**Participant B provides context:**

```text
BUTTERFLY/0.1
TYPE: SYNC
FROM: B
TO: A
TASK: shared-analysis
REF: sync-001-response

CONTENT:
The available source describes a proposal.
I have found no evidence of formal approval.

The distinction should be preserved in the
shared analysis.
```

**Participant A checks the interpretation:**

```text
BUTTERFLY/0.1
TYPE: CHECK
FROM: A
TO: B
TASK: shared-analysis
REF: check-001

CONTENT:
Understood. I will classify the statement
as a proposal, with approval status unknown.
Is that consistent with your source?
```

The human chooses whether to forward each message.

## 8. Experimental evidence

### BF-SYNC-001

A human-initiated, targeted information retrieval test demonstrated that information missing from one conversation could be recovered from another.

The exchange preserved relevant original wording and distinguished factual material from inference.

**Observed result:** PASS for targeted retrieval.

Autonomous detection of missing context and general completeness were not demonstrated.

### BF-SYNC-002

A targeted exchange exposed ambiguity about the provenance and status of a decision-related statement.

A follow-up clarified whether the material represented a fact, intention, proposal or approval.

**Observed result:** Targeted provenance clarification demonstrated.

The broader benefits of independent source reasoning and the coordination cost of the process remain open to evaluation.

## 9. Limitations and open questions

Butterfly v0.1 does not guarantee:

- Accurate or complete AI responses.
- Independent verification of forwarded claims.
- Detection of every missing assumption.
- Message delivery or authenticity.
- Secure transport.
- Confidentiality of information shared through an external channel.
- Automatic execution or autonomous communication.
- Agreement between participants.

Open questions include:

**OQ-001: Participant Identity and Naming**

How should participant identity, conversation identity and transport identity be represented and distinguished?

**OQ-002: Transport and Security**

What responsibilities belong to the protocol, and what must be provided by the communication channel?

**OQ-003: Interoperability**

How does the protocol behave across different AI models, providers and multiple human intermediaries?

**OQ-004: Evaluation**

Under what conditions does Butterfly improve collaboration enough to justify its coordination overhead?

These identifiers, apart from the previously established OQ-001, are provisional.

## 10. Next steps

1. Review and validate the proposed message format.
2. Run an end-to-end exchange between two independent conversations.
3. Record the actual messages, human interventions and outcomes.
4. Test CHECK behaviour explicitly.
5. Refine the specification based on observed results.

---

*Lazy & Bald Software Corporation is a fictional name used for historical and humorous purposes. It is not a registered company or legal entity.*

*Management responsibilities: classified.*
