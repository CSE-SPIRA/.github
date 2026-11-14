🏠 SPIRA

Your order arrives. Your home is already prepared.

26-2 Hanyang University Software Engineering · AI & Applications Project

<!-- TODO: hero image (service overview or app screenshot), 16:9 --> <!-- <img width="100%" alt="SPIRA overview" src="TODO-hero-image" /> --> <br/>
📄 Documentation

SPIRA: Proactively Preparing Smart Homes via Retrieval-Augmented Purchase Intent Inference over Synthetic Knowledge

Software Engineering (CSE406)
SPIRA_SE Paper (PDF)
LaTeX Source (.tex)
AI & Applications (ITE351)
SPIRA_AI Paper (PDF) — TODO
Synthetic Knowledge Base design — SPIRA_KB
<br/>
💡 Proposal

Online delivery brings products to the door, but the user still has to prepare the home for what those products are for. Smart-home routines can automate the work only after the user has recognized the situation and set up the rules.

SPIRA reads the items in an order screenshot the user shares, retrieves similar purchase cases from a synthetic purchase-intent knowledge base, and judges what the order is for. When there is an intent, SPIRA prepares the home with appliances and IoT devices without asking, announcing the preparation once with a single card.

For example, party supplies, cupcake mix, and strawberries ordered on Thursday night are read as a child's birthday party on Saturday. When the package is brought in, the fridge screen shows "Wash the strawberries right before decorating." On Saturday, the living room is cleaned and a child-safety mode turns on before guests arrive, the lights and TV switch to a princess theme when they arrive, and the oven waits with the cupcake setting.

Our approach focuses on three core ideas:

Synthetic purchase-intent knowledge: Real household purchase records are scarce before launch. LLM agents generate order cases from a fixed list of 30 intents, two models from different companies label each order blindly, and only batches that pass a quality gate are loaded into the knowledge base. Most orders are ordinary shopping, so no intent, no tasks is a normal result.
Prepare without asking, within safe bounds: The home acts only at two moments, the time of the intended event and the moment a package is brought in. The LLM judges the intent and proposes tasks; code finds the time, restricts tasks to the devices this home has, and turns anything costly, dangerous, or irreversible (such as starting the oven) into a standby that a person starts.
The user's reactions shape the next preparation: The user can stop a preparation or switch off a single line on the card. The Home Hub reads back actual device state and does not overwrite what a person changed. Stops, switched-off lines, and manual changes are kept as household memory and applied to the next preparation for the same intent.
<br/>
🔧 Architecture Design
<!-- TODO: architecture image (same figure as ARCHITECTURE.md) --> <!-- <img width="100%" alt="SPIRA architecture" src="TODO-architecture-image" /> -->
The user shares an order screenshot to the SPIRA App (Flutter).
The SPIRA Server (FastAPI) extracts the items, retrieves similar cases from the synthetic purchase-intent knowledge base (PostgreSQL + pgvector, BGE-M3 embeddings), and judges the intent with an LLM.
The Server turns the intent into tasks for this home's devices and confirms a versioned plan; the App shows it as one card for this preparation.
The Home Hub pulls the plan, waits for each trigger, checks the current state, executes, reads the result back, and restores what it changed unless a person changed it.
Devices are a virtual household simulator (MQTT) with a 2D viewer, plus a physical Tapo light.
Execution results and user reactions return through the Server to the same card and are stored as household memory.
<br/>
🎥 Demo Video
<!-- TODO: replace with YouTube thumbnail link --> <!-- [<img width="100%" alt="SPIRA demo video" src="TODO-video-thumbnail" />](TODO-youtube-link) -->

Coming soon.

<br/>
📦 Repositories
Repository	Contents
SPIRA	SPIRA Service · Home Hub · App · Simulator · shared contracts
SPIRA_KB	Synthetic purchase-intent case pipeline and embedding package
<br/>
🔗 Links
Slides: TODO
Blog: TODO
<br/>
👥 Team Members
Name	Organization	Email
Jeewon Lee	Hanyang University Dept. of Information Systems, Seoul, Republic of Korea	leejeewon916@gmail.com
Uijin Lee	Hanyang University Dept. of Information Systems · Dept. of Food & Nutrition, Seoul, Republic of Korea	smilelejn@gmail.com
Seojin Lee	Hanyang University Dept. of Information Systems, Seoul, Republic of Korea	leeseojini0303@gmail.com
Yejoon Kim	Hanyang University Dept. of Information Systems, Seoul, Republic of Korea	yejoonkim1340@gmail.com
