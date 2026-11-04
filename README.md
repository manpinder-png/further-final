# Further — find someone to learn with now

A learner knows the question they want to ask. The person who could help might describe the same idea in completely different words. **Further turns that question into a live invitation to learn together.** Two people choose a starting point, explain it to each other, and leave with a way to check what they understood.

**Meta Global AI Developer Hackathon · Build for Your World · v5**

[Run Further](docs/ONBOARDING.md) · [Architecture and diagrams](docs/ARCHITECTURE.md) · [Code and dependencies](docs/CODE_MAP.md)

## What we entered and what you can try

Our application proposed making it as easy to find a learning partner as to join a multiplayer game. The first audience is an adult technical community. The example we entered was someone who finds GPUs a black box. Here is how that idea works in the prototype.

| In the application | In Further |
|---|---|
| Arrive with a rough question | Ask why a graphics card trains an AI model faster than a general-purpose processor. The Path guide delegates a reading of the learner's intent, then proposes a small map of concepts to explore. The learner sees which agent is working as the result streams. |
| Find someone with a related question and time to talk | Open Geomind. Two people can use different words and have different concept IDs. Available, opted-in learners appear near you when the mathematical similarity of their active concepts clears the discovery threshold. Refresh to check again, or keep learning independently while waiting. |
| Learn through conversation | Select a person and a topic pair. Both participants accept before the shared room opens. Each can explain, challenge an example, and ask the learning companion for a prompt. The solo explain-back lets a learner try an answer in their own words. |
| Build on the encounter | Reopen a question or zoom through **My knowledge map** to revisit saved concepts across questions. A future pilot would measure time to a mutually accepted match, perceived usefulness, independent explanations, and repeat participation. |

## How a question becomes a mathematical match

1. **Interpret.** The knowledge-map agent reads the learner's saved map and calls the metadata specialist. The backend validates the proposed concepts and relationships before saving them.
2. **Index changes.** Saving changed learning records queues durable work. A local Meta RoBERTa encoder converts each changed concept's title and short description into a versioned 768-dimensional vector. Separate private indexes support the learner's own searches.
3. **Find a person.** On discovery, PostgreSQL with pgvector compares fresh active-concept vectors by cosine distance. It considers consent, current availability, language and other eligibility rules. Geomind places people by conceptual similarity. Peer recommendations also weigh reviewed explanations and time fit. A pending index has a visible waiting state.
4. **Let people decide.** Each result can show the two topics that brought the learners together. The server rechecks eligibility on invitation. Each person controls whether to meet. [Matching policy and evaluation](docs/GEOMIND.md)

## Where Meta runs

| Model and provider | Job in Further |
|---|---|
| Muse Spark 1.3 · Meta Model API | Default for mapping, lessons, facilitation, image understanding and grounded resource discovery. |
| Muse Spark Open · Baseten | Selectable metadata specialist. The hackathon endpoint uses exactly `meta-models/muse-spark-open-1026`. |
| Muse Voice Transcribe · Meta Model API | Turns a recorded question into editable text. |
| RoBERTa base · local CPU | Encodes concepts for semantic discovery and private learning records for owner search. Aurora PostgreSQL stores the shared vectors. |

The team also used **Meta Muse Wonder alongside Codex during development**. Wonder is available as an optional runtime map-model override. The OpenAI SDK carries requests to the selected Meta or Baseten endpoint. [Meta model catalog](https://dev.meta.ai/docs/models) · [Agent contracts and model routes](docs/agents/README.md)

## Evidence for review

| Judging criterion | What to review |
|---|---|
| Impact · 30% | Two learners can discover a related question and explain an idea together. The next pilot question is whether that exchange was useful enough for both to return. |
| Use of Meta AI tooling · 25% | Follow one request from Meta interpretation to validated learning records, then local Meta embeddings. [Architecture](docs/ARCHITECTURE.md) |
| Technical depth and execution · 20% | Inspect agent delegation, incremental indexing, rank computation, and the two-party handshake. [Dependency map](docs/CODE_MAP.md) · [Automated tests](tests/) |
| Demo · 25% | Try peer discovery, mutual acceptance and the shared room from two accounts. [Two-person setup](docs/ONBOARDING.md#6-two-person-live-test) |

The near-term opportunity is technical learning. The same idea could help an on-call engineer find a colleague investigating a related symptom, or a field technician find someone working through a similar repair. Those are directions to test. [Official judging guide](https://cerebralvalley.ai/e/meta-ai-developer-hackathon/details#8-judging-process-16)

## Run the prototype

Each developer runs the Next.js UI, backend, agent runtime and encoder locally. Two machines can share Cognito identity, Aurora PostgreSQL with pgvector, and private S3 media. An isolated PGlite mode is also available. Follow the setup guide for the correct credentials and commands. [Onboarding](docs/ONBOARDING.md) · [Developer handoff](docs/HANDOFF.md) · [Source credits](SOURCE.md)
