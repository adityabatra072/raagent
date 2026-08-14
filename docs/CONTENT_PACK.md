# RunAnywhere Agent, Launch Content Pack

Nine days of content. One self-contained piece per day. Every demo in this pack is
real in the current build or is labeled NEEDS SETUP with the exact steps.

Replace `[REPO LINK]` with the GitHub URL and `[SITE LINK]` with runanywhere.ai
before publishing. Nothing else in the posts is a placeholder.

---

## The angle

The recurring headline, in whatever words fit the day:

> On-device AI was considered a novelty. "Hey, it can run on your phone."
> It now runs complete agentic systems.

The enemy is one assumption: that agents need the cloud. Every piece attacks that
assumption with a working demo, not an argument.

Variations to rotate so the feed does not repeat itself:

- "A 2.6B model on a phone CPU is not a toy. It is an operator."
- "The phone is not a thin client anymore."
- "Agents were supposed to need a datacenter. This one needs a pocket."
- "Small model, real tools, no server."

### Facts you may cite (all verifiable, use as market context only)

- Apple Intelligence requires an iPhone 15 Pro or newer. A base iPhone 15 gets none of it.
- Apple's LLM Siri rewrite is Gemini running on Private Cloud Compute. It is a cloud
  product and it has not shipped to consumers.
- Apple settled a lawsuit for roughly $250M over the personal-context Siri demo it
  advertised in 2024 and never delivered.
- That exact demo (remember my medication and my therapist, recall it later) runs
  offline in RunAnywhere Agent today.

Do not present our demo device as any specific phone model. Referencing Apple's
device-exclusion policy as a market fact is fine.

### Hard rules (from the adversarial demo review, these are law)

1. Never demo something Siri does well. No timers, no "open Spotify" as a hero beat,
   no plain reminders.
2. Never demo world knowledge. A 2.6B model will hallucinate and the audience will
   compare it to ChatGPT.
3. Never claim it controls any app. We name our tools honestly.
4. Latency is narrated, never apologized for. Every video either shows real time with
   the action rail as the story, or carries a caption stating it is condensed and
   giving the real turn time.
5. The tool counts, the model judges. Gap-finding, clock arithmetic, and track
   resolution are computed in code. Say so. It is engineering maturity and it is why
   the demos hold up on a small model.

### Production notes (apply to every video)

- Vertical, 30 to 90 seconds, captions burned in. Assume sound off on X, sound on
  optional everywhere.
- The action rail is the protagonist. Frame it. Each tool call ticking through is the
  proof that this is an agent and not a chatbot.
- Every offline demo opens with the airplane-mode toggle, full screen, no cut between
  the toggle and the first utterance. This is the anti-staging shot.
- Standing latency caption for condensed cuts: "Condensed. Real turn: NN seconds on a
  phone CPU. No server involved." Fill NN with the actual measured time from the take.
- Standing latency line for real-time cuts: "This is real time on a phone CPU."
- End card for every video: app name, "Open source", `[REPO LINK]`.
- No emojis in captions or posts. No em dashes anywhere.

---

## Day 1: Ninety Minutes

**Hook:** Tell your phone "find me 90 minutes tomorrow, not before 10am, not right
after standup, and put it in." Airplane mode on. It does it.

**Feasibility: WORKS TODAY.** This is the demo already being recorded.

### Storyboard

Setup checklist:

- Model loaded (open the app once before recording, first load takes about 30s)
- Calendar permission granted
- Tomorrow's calendar seeded: Standup 09:30 to 10:00, Design review 11:00 to 12:00,
  1:1 15:00 to 15:30
- Chat cleared, airplane mode ready to toggle on camera

Exact utterance:

> "Look at tomorrow. Find me 90 minutes for the gym that isn't before 10am and isn't
> straight after standup, and put it in."

Expected tool chain:

1. `calendar_query("tomorrow")` returns events plus precomputed free gaps
   (e.g. "12:00 to 15:00, 180 min")
2. Model picks the gap that satisfies both constraints
3. `calendar_create(title, start, end)`

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Finger flips airplane mode on, no cut | "Airplane mode. No cloud for the rest of this video." |
| 2 | 6s | Typing or speaking the utterance | "Two constraints. Both opinions, not filters." |
| 3 | 15s | Action rail: reading calendar, gaps listed | "The tool computes the free gaps. The model judges them." |
| 4 | 10s | Rail: event being created, confirmation | "Condensed. Real turn: NN seconds on a phone CPU." |
| 5 | 8s | Cut to the system Calendar app, the gym block sitting between real events | "It wrote it to the real calendar." |
| 6 | 5s | Model pill showing on-device badge, end card | "2.6B params. Runs on the phone. Open source." |

### X thread

Tweet 1:
> Airplane mode on. I told my phone: find me 90 minutes for the gym tomorrow, not
> before 10am, not straight after standup, and put it in.
>
> A 2.6B model running on the phone CPU read my calendar, picked the right gap, and
> wrote the event. No server touched this.

Tweet 2:
> How it holds up on a small model: the calendar tool returns events plus precomputed
> free gaps. The model's only job is judgment, "which gap satisfies both constraints."
> Code does arithmetic. The model makes the call. That division of labor is the whole
> trick.

Tweet 3:
> Video is condensed. The real turn took about NN seconds on a phone CPU, and the app
> shows you every step while it runs. Open source: [REPO LINK]

### LinkedIn post

> On-device AI was considered a novelty. "Hey, it can run on your phone." It now runs
> complete agentic systems.
>
> This video is a 2.6B-parameter model (LiquidAI LFM2.5, GGUF via llama.cpp) running
> on a phone CPU, in airplane mode, doing something no shipping assistant does: "find
> me 90 minutes tomorrow that isn't before 10am and isn't straight after standup, and
> put it in."
>
> That sentence contains two constraints expressed as opinions. The agent reads the
> calendar through a tool that precomputes free gaps, judges which gap satisfies both
> constraints, and writes the event back. Code does the clock arithmetic. The model
> does the judgment. That split is why a small model does this reliably.
>
> Honest numbers: a turn takes 15 to 45 seconds on device. The video is condensed and
> says so. We think watching an agent think on your own hardware, with no network, is
> worth the wait.
>
> RunAnywhere Agent is open source: [REPO LINK]

---

## Day 2: The Demo Apple Paid $250M to Not Ship

**Hook:** Apple advertised "remember my medication, recall it later," never shipped
it, and settled a lawsuit over it. It runs offline in this app. Then we kill the app
and it still remembers.

**Feasibility: WORKS TODAY.**

### Storyboard

Setup checklist:

- Model loaded, chat cleared, airplane mode on camera
- Calendar permission granted
- App switcher rehearsed for a clean on-camera force-kill

Exact utterances:

> "Remember that I'm on 20mg of Lexapro, my therapist is Dr. Okafor, and my
> appointment is Thursday at 4pm."

Then, after force-killing and reopening the app:

> "What do I need to remember about Thursday?"

Expected tool chain:

1. `remember(fact)` then `calendar_create(title="Dr. Okafor", start=Thursday 4pm)`
2. After the kill: `recall(query)` returns the dosage, the name, and the time

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Airplane mode toggle | "No network for any of this." |
| 2 | 7s | The remember utterance being spoken | "Apple demoed this feature in 2024. It never shipped. They settled for ~$250M." |
| 3 | 12s | Rail: Saving to memory, Saved on this phone. Adding Dr. Okafor to calendar | "Stored as a file on this phone. There is no request to inspect because there is no request." |
| 4 | 5s | App switcher, app swiped away, killed | "Now we kill the app." |
| 5 | 12s | App reopened, recall question, rail ticks, answer names the dosage, the doctor, 4pm | "Condensed. Real turn: NN seconds on a phone CPU." |
| 6 | 6s | End card | "Fully local memory. Delete the app and it is gone. Open source." |

### X thread

Tweet 1:
> In 2024 Apple advertised a Siri that remembers your personal context. It never
> shipped. Apple settled for about $250M over that ad.
>
> Here is that exact demo running offline, on a phone CPU, in an open-source app.

Tweet 2:
> "Remember I'm on 20mg of Lexapro, my therapist is Dr. Okafor, appointment Thursday
> at 4pm." Saved to local memory, appointment written to the calendar. Then I
> force-kill the app. Reopen. "What do I need to remember about Thursday?" It answers
> with all three facts.

Tweet 3:
> The memory is a file on the phone. No account, no sync, no server log. Delete the
> app and everything you told it is gone. That is the privacy model: physics, not
> policy. [REPO LINK]

### LinkedIn post

> The most expensive AI demo in history is one Apple never shipped. The 2024 ad showed
> Siri remembering personal context. The feature was delayed indefinitely and Apple
> settled the false-advertising suit for roughly $250M.
>
> That demo runs today in RunAnywhere Agent, offline, on a phone CPU.
>
> Tell it your medication, your therapist's name, your appointment. A 2.6B model calls
> a remember tool and a calendar tool. The facts land in a local store and in your
> real calendar. Force-kill the app, reopen it, ask what you need to remember about
> Thursday. It answers with all three facts.
>
> There is no server request to inspect because there is no server request. The
> privacy guarantee is not a policy document. It is the absence of a network path.
>
> Turns take 15 to 45 seconds on device and the app narrates every tool call while you
> wait. We think that trade is right for the most sensitive sentences you will ever
> say to a computer.
>
> Open source: [REPO LINK]

---

## Day 3: Teach Your Phone a Verb

**Hook:** "New rule: when I say wind down, dim the screen, kill the flashlight,
remind me to set my alarm." Two minutes later you say "wind down" and all three
happen at once.

**Feasibility: WORKS TODAY.**

### Storyboard

Setup checklist:

- Model loaded, chat cleared, airplane mode on camera
- Flashlight turned on before recording so the macro visibly kills it
- Screen brightness high so the dim is visible on camera
- Notification permission granted

Exact utterances:

Teaching:
> "New rule: when I say wind down, set the brightness to 20 percent, turn the
> flashlight off, and remind me to set my alarm."

Executing:
> "Wind down."

Expected tool chain:

1. `define_macro(name="wind down", steps=[set_brightness, flashlight, send_notification])`
2. On "wind down": `run_macro("wind down")`, all three steps replay deterministically

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Airplane mode toggle, torch visibly on | "Offline. Torch on. Watch it." |
| 2 | 8s | The teaching utterance | "No Shortcuts editor. No blocks. A sentence." |
| 3 | 10s | Rail: macro defined with three steps listed | "The model records the steps once. Replay is deterministic code." |
| 4 | 3s | "Wind down." typed or spoken | "Two minutes later." |
| 5 | 8s | Wide shot of the phone: screen dims, torch dies, notification banner lands | "This is real time. All three fired from one word." |
| 6 | 6s | End card | "The macro is a file on this device. Open source." |

### X thread

Tweet 1:
> I programmed my phone by talking to it.
>
> "New rule: when I say wind down, set brightness to 20 percent, turn the flashlight
> off, and remind me to set my alarm."
>
> Then I said "wind down." Screen dimmed, torch died, reminder landed. Offline, on a
> 2.6B model.

Tweet 2:
> Engineering note: the model plans the steps once, at teach time. Saying the verb
> replays them as deterministic code. A small model re-planning four actions on every
> invocation would be slow and would drift. Teach once, replay forever.

Tweet 3:
> Siri cannot learn a new verb. Shortcuts can, if you open an editor and drag blocks.
> Here the editor is a sentence and the macro is a file on your phone. [REPO LINK]

### LinkedIn post

> End users have never been able to program their phones by speaking. Shortcuts exists
> and almost nobody builds them, because the editor is the barrier.
>
> In RunAnywhere Agent you say: "New rule: when I say wind down, set the brightness to
> 20 percent, turn the flashlight off, and remind me to set my alarm." A 2.6B model
> running on the phone parses that into a named macro with three tool steps.
>
> Later you say "wind down" and the three steps replay. The design decision that makes
> this work on a small model: the LLM plans once, at teach time. Execution is
> deterministic replay, not re-planning. Fast, repeatable, no drift.
>
> The macro is a file on the device. It works in airplane mode. It survives app
> restarts. Nobody's server knows your evening routine.
>
> Open source: [REPO LINK]

---

## Day 4: The Phone That Wakes Itself

**Hook:** Tell the agent to check something again in 3 minutes and judge the result.
Walk away. The phone wakes itself, runs a fresh agent loop, and notifies you.

**Feasibility: WORKS TODAY.**

### Storyboard

Setup checklist:

- Model loaded, chat cleared, airplane mode on camera
- Notification permission granted, Do Not Disturb off
- Battery between 30 and 80 percent so there is room for a delta
- App stays foregrounded for the wake (iOS suspends background apps; overdue tasks
  run on next launch). Keep the agent screen up for the whole take.

Exact utterance:

> "Check my battery now and remember it. Then in 3 minutes check it again and tell me
> if it dropped more than 2 percent."

Expected tool chain:

1. `device_info` then `remember("battery was N%")` then
   `schedule_task(instruction, when="+3")`
2. Three minutes later, unattended: a fresh agent loop runs
   `device_info` then `recall` then compares then `send_notification`

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Airplane mode toggle | "Offline. And about to be unattended." |
| 2 | 8s | The utterance | "One sentence. Three instructions, one of them for the future." |
| 3 | 12s | Rail: battery read, fact remembered, task scheduled | "It wrote the number down and set itself an appointment." |
| 4 | 4s | Hands leave frame. Phone alone on the desk, timestamp overlay | "Nobody touches the phone from here." |
| 5 | 15s | Time-skip. A bordered scheduled-task card appears in chat by itself, rail ticks through a fresh run, notification drops | "That is the model waking itself up, re-reading its own note, and making a judgment call." |
| 6 | 6s | End card | "Siri can trigger on a threshold. It cannot schedule reasoning. Open source." |

### X thread

Tweet 1:
> I told my phone: check the battery now and remember it, then in 3 minutes check
> again and tell me if it dropped more than 2 percent.
>
> Then I put it down. Three minutes later it woke itself, ran a fresh agent loop,
> compared against the number it wrote down, and sent a notification. Offline.

Tweet 2:
> This is the capability gap in one demo. A Shortcuts automation can trigger on a
> battery threshold. It cannot record a baseline because you said a sentence, and it
> cannot decide at fire time what "dropped more than 2 percent" means. Scheduled
> reasoning is a different category from scheduled triggers.

Tweet 3:
> Honest limit: iOS suspends background apps, so the wake fires while the app is
> alive, and overdue tasks run on next launch. That is an OS constraint, not a model
> one. Everything else is a 2.6B model on a phone CPU. [REPO LINK]

### LinkedIn post

> Every assistant on the market executes commands in the present tense. The
> interesting frontier is deferred agency: give the agent an instruction about the
> future and have it carry that instruction out unattended.
>
> Demo: "Check my battery now and remember it. Then in 3 minutes check it again and
> tell me if it dropped more than 2 percent." RunAnywhere Agent reads the battery,
> writes the number to local memory, and schedules itself a task. Three minutes later
> the app wakes itself and runs a fresh agent loop with the full tool set: read the
> battery again, recall the baseline, compare, notify.
>
> The comparison is not a precompiled rule. The model interprets "dropped more than 2
> percent" at fire time, against a fact it recorded because of a sentence you said.
> Shortcuts triggers cannot do that. Siri cannot do that.
>
> Constraint we state plainly: iOS suspends background apps, so wakes fire while the
> app is alive, and overdue tasks run on next launch.
>
> All of it offline, on a 2.6B model. Open source: [REPO LINK]

---

## Day 5: One Sentence, Two Companies' Software

**Hook:** "Find 30 free minutes on my calendar tomorrow, book a meeting called Design
sync, invite priya@gmail.com, then message Priya on Slack with the time." One
sentence, four tool calls, two SaaS products, orchestrated by a model in your pocket.

**Feasibility: NEEDS SETUP.** Requires a hosted MCP server exposing Google Calendar
and Slack.

### Setup steps (do once, about 15 minutes)

1. Create an account at composio.dev and open the dashboard.
2. Enable two toolkits: Google Calendar and Slack. Complete the OAuth connection for
   each (your Google account, your Slack workspace).
3. Create an MCP server from those two toolkits. Keep the exposed action list small:
   calendar list events, calendar create event, Slack send message. Small models
   route better across 5 tools than 50. Composio hosts the server and gives you a
   streamable HTTP URL.
4. Copy the server URL and the API key. Note the exact auth header name shown in the
   Composio dashboard for MCP access (typically `x-api-key`).
5. In RunAnywhere Agent: Tools screen, Add MCP server, paste the URL, enter the
   header name and key, save. The server's tools appear in the agent's tool list.
6. Dry run before recording: ask "list my Slack channels" and approve the call. Every
   MCP call is approval-gated, so rehearse the tap rhythm.

Zapier MCP (mcp.zapier.com) or Pipedream work the same way: build a server with the
same three actions, copy the streamable HTTP endpoint and its auth header into the
Tools screen.

### Storyboard

Setup checklist:

- MCP server configured as above and dry-run tested
- Network ON (say so on screen; this demo is about reach, not airplane mode)
- Google Calendar seeded with 2 or 3 real-looking events tomorrow
- A Slack DM or channel where the message will visibly land, second device or
  desktop ready to show it

Exact utterance:

> "Find 30 free minutes on my calendar tomorrow, book a meeting titled Design sync,
> invite priya@gmail.com, and then message Priya on Slack with the time."

Expected tool chain:

1. MCP: Google Calendar list events (tomorrow)
2. Model finds a 30-minute gap
3. MCP: Google Calendar create event with attendee
4. MCP: Slack send message with the booked time

Each call pauses on an approval card. The approvals are part of the story, show them.

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 5s | The utterance | "One sentence. Two companies' software." |
| 2 | 6s | Tools screen scroll-by showing the MCP server entry | "Any MCP server, added by URL. This one is Google Calendar plus Slack." |
| 3 | 12s | Rail: calendar read, approval card, tap approve | "Every external call stops for approval. You are the loop." |
| 4 | 12s | Rail: event created with invite, approval card, Slack message sent | "Condensed. Full run: about N minutes of on-device turns." |
| 5 | 8s | Desktop or second phone: Google Calendar shows the event, Slack shows the message | "Both landed. Orchestrated by a 2.6B model on a phone." |
| 6 | 6s | End card | "MCP client built in. Bring your own servers. Open source." |

### X thread

Tweet 1:
> "Find 30 free minutes on my calendar tomorrow, book a meeting titled Design sync,
> invite priya@gmail.com, then message Priya on Slack with the time."
>
> One sentence. Four tool calls. Google Calendar and Slack, orchestrated by a 2.6B
> model running on my phone.

Tweet 2:
> Why a small model does this reliably: it is orchestration, not world knowledge. The
> app is an MCP client. Add any streamable HTTP MCP server by URL from the Tools
> screen (Composio, Zapier, Pipedream, or self-hosted) and its tools appear in the
> agent. Every call is approval-gated.

Tweet 3:
> The model plans the chain and fills the arguments. The servers do the work. You
> approve each side effect. That is what an agent should be: judgment on your device,
> execution under your thumb. [REPO LINK]

### LinkedIn post

> The standard objection to on-device AI: "a small model can't know enough to be
> useful." Correct, and it does not matter, because agent work is mostly
> orchestration, not knowledge.
>
> Demo: "Find 30 free minutes on my calendar tomorrow, book a meeting titled Design
> sync, invite priya@gmail.com, then message Priya on Slack with the time." That is a
> chain of four tool calls across Google Calendar and Slack. A 2.6B model on a phone
> CPU plans the chain, picks the gap, fills the arguments, and stops for your approval
> before every external call.
>
> The plumbing is MCP. RunAnywhere Agent is an MCP client: paste any streamable HTTP
> server URL and auth header into the Tools screen and its tools join the agent.
> Hosted providers like Composio and Zapier put Slack, Google Calendar, GitHub, and
> hundreds of other systems one URL away. Setup for this demo took 15 minutes.
>
> The turns take seconds each on a phone CPU and the video is condensed. What you are
> watching is the reasoning happening in your pocket while the SaaS does the labor.
>
> Open source: [REPO LINK]

---

## Day 6: E.V, Hands Free

**Hook:** Say a wake phrase, ask a question with real judgment in it, get a spoken
answer. Speech to text, agent loop, text to speech, all running on the phone, in
airplane mode.

**Feasibility: WORKS TODAY.**

### Storyboard

Setup checklist:

- Model loaded, hands-free mode enabled, chat cleared
- Airplane mode on camera
- Calendar seeded with tomorrow's events (reuse Day 1 seed)
- Quiet room, phone propped up, hands visibly off the phone for the whole take
- Record device audio or mic the phone speaker clearly, the spoken answer is the payoff

Exact utterance (spoken, no hands):

> "E.V, look at tomorrow afternoon and tell me my longest free stretch."

Expected tool chain:

1. On-device Whisper transcribes the utterance
2. `calendar_query("tomorrow")` returns events plus precomputed free gaps
3. Model picks the longest afternoon gap
4. Answer spoken via on-device Piper TTS

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Airplane mode toggle, phone propped, hands leave frame | "Offline. Hands off from here." |
| 2 | 6s | Speaker says the wake phrase and question, waveform or mic indicator on screen | "Whisper transcribes on the phone. Nothing leaves it." |
| 3 | 14s | Rail: calendar read, gaps listed, answer forming | "Real time. The pause is a 2.6B model thinking on a phone CPU." |
| 4 | 8s | Phone speaks the answer, captioned verbatim | "Piper speaks the answer. Also on the phone." |
| 5 | 6s | End card | "Wake phrase to spoken answer, zero packets. Open source." |

### X thread

Tweet 1:
> "E.V, look at tomorrow afternoon and tell me my longest free stretch."
>
> Airplane mode. The phone heard me (on-device Whisper), reasoned over my calendar
> (2.6B model, on-device), and spoke the answer (on-device Piper). Not one packet
> left the device.

Tweet 2:
> Every voice assistant you have used ships your voice to a server. This whole loop,
> wake phrase, transcription, agent reasoning, tool call, speech synthesis, runs on
> the phone. The pause you see is real: this is real time on a phone CPU. We show it
> because it is the proof.

Tweet 3:
> The question matters too. "Longest free stretch tomorrow afternoon" is judgment over
> your data, not trivia. That is the class of question worth answering locally.
> [REPO LINK]

### LinkedIn post

> Voice assistants normalized a strange bargain: to ask your phone anything, you ship
> your voice to a datacenter.
>
> This demo runs the entire loop on the handset. Wake phrase ("E.V"), on-device
> Whisper for speech to text, a 2.6B model driving an agent loop with tool calls, and
> on-device Piper for the spoken answer. The video shows airplane mode going on first
> and hands leaving the frame.
>
> The question is chosen deliberately: "look at tomorrow afternoon and tell me my
> longest free stretch." That needs the agent to read the calendar through a tool that
> precomputes free gaps and then judge among them. Judgment over your own data is
> exactly the workload that belongs on your own hardware.
>
> We publish the pause. The answer takes seconds to form on a phone CPU and we would
> rather show real time than pretend otherwise.
>
> Open source: [REPO LINK]

---

## Day 7: Point the Camera, Get an Agent

**Hook:** Attach a photo of a thing. "What is this and remind me to buy it
tomorrow." One agentic run: vision model describes it, agent remembers it, reminder
lands on your calendar. Offline.

**Feasibility: WORKS TODAY.**

### Storyboard

Setup checklist:

- Model loaded, chat cleared, airplane mode on camera
- A distinctive physical object with a readable identity (a specific coffee bag, a
  vitamin bottle, a book). Avoid objects that need brand-level world knowledge to
  identify; the vision model is SmolVLM-500M and honest framing beats a flub.
- Photo taken in good light before or during the take
- Calendar and notification permissions granted

Exact utterance (with the photo attached):

> "What is this, and remind me to buy it tomorrow morning."

Expected tool chain:

1. `describe_image` (on-device SmolVLM-500M) returns a description
2. `remember("need to buy: ...")`
3. `calendar_create` or `send_notification` scheduled for tomorrow morning

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 4s | Airplane mode toggle | "Offline, including the vision model." |
| 2 | 6s | Photo of the object being attached, utterance typed | "One request: identify it and act on it." |
| 3 | 12s | Rail: describe_image running, description appears | "SmolVLM-500M, running on the phone, tells the agent what it sees." |
| 4 | 10s | Rail: fact remembered, reminder created for tomorrow morning | "Condensed. Real run: NN seconds on a phone CPU." |
| 5 | 6s | Calendar or notification center showing tomorrow's reminder | "Seen, understood, scheduled. One run." |
| 6 | 5s | End card | "Two models, one phone, no cloud. Open source." |

### X thread

Tweet 1:
> Attached a photo to my phone's agent and typed: "what is this, and remind me to buy
> it tomorrow morning."
>
> A 500M vision model identified it. The 2.6B agent model remembered it and put the
> reminder on tomorrow's calendar. One run. Airplane mode the whole time.

Tweet 2:
> Two models cooperating on one phone: SmolVLM-500M answers "what am I looking at,"
> the LLM decides what to do about it. The vision output is just another tool result
> in the agent loop. Real run took about NN seconds on a phone CPU; the video is
> condensed and says so. [REPO LINK]

### LinkedIn post

> Multimodal agents are assumed to be a datacenter product. Here is one on a phone,
> in airplane mode.
>
> Attach a photo, type "what is this, and remind me to buy it tomorrow morning." The
> agent calls a describe_image tool backed by SmolVLM-500M running on the device. The
> description comes back as a tool result, the 2.6B agent model remembers the item
> and schedules the reminder. Perception, memory, and action in a single agentic run,
> with no network path.
>
> Scope, stated honestly: a 500M vision model describes what it sees. It will name a
> coffee bag; it will not recognize your specific rare vintage. We pick demos that
> respect what the model is, and it delivers on those every time.
>
> The run takes under a minute on a phone CPU and the app shows each step as it
> happens.
>
> Open source: [REPO LINK]

---

## Day 8: The Morning Standup Ran From My Pocket

**Hook:** "Check the open pull requests on our repo, then post a summary to the
dev channel on Slack." GitHub and Slack, chained by a model on the phone, every call
approved by a human thumb.

**Feasibility: NEEDS SETUP.** Requires a hosted MCP server exposing GitHub and Slack.

### Setup steps (do once, about 15 minutes)

1. Go to mcp.zapier.com and create an MCP server.
2. Add three actions: GitHub find pull requests (or list issues), GitHub get pull
   request detail, Slack send channel message. Connect your GitHub account and Slack
   workspace when prompted. Keep the action list to these three; small models route
   better across few tools.
3. Select the streamable HTTP transport. Copy the endpoint URL and the bearer token.
   The header is `Authorization: Bearer <token>` as shown in the Zapier dashboard.
4. In RunAnywhere Agent: Tools screen, Add MCP server, paste the URL, enter the
   header name and value, save.
5. Dry run: "list open pull requests on <owner>/<repo>" and approve the call. Confirm
   the Slack action posts to the intended channel before recording.

Composio works identically: enable the GitHub and Slack toolkits, build the server,
copy its URL and API key header into the Tools screen.

### Storyboard

Setup checklist:

- MCP server configured and dry-run tested
- Network ON, say so on screen
- A repo with 2 or 3 genuinely open PRs with real titles
- Slack channel visible on a second screen for the payoff shot

Exact utterance:

> "Check the open pull requests on runanywhere's repo, then post a one-line summary
> of each to the dev channel on Slack."

Expected tool chain:

1. MCP: GitHub list open pull requests
2. Model writes one-line summaries from the titles and metadata returned by the tool
   (summaries come from tool output, not from world knowledge)
3. MCP: Slack send channel message

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 5s | The utterance | "GitHub and Slack. One sentence, from a phone." |
| 2 | 10s | Rail: PR list call, approval card, approve | "The agent asks before it touches anything external." |
| 3 | 12s | Rail: model drafting the summary from tool output | "It summarizes what the tool returned. No guessing, no world knowledge." |
| 4 | 10s | Approval card for the Slack post, approve, sent | "Condensed. Real chain: a few minutes of on-device turns." |
| 5 | 8s | Desktop Slack: the summary message in the channel | "Landed. Written by a 2.6B model in a pocket." |
| 6 | 5s | End card | "MCP client, approval-gated, open source." |

### X thread

Tweet 1:
> Morning triage, from a phone, no laptop:
>
> "Check the open pull requests on our repo, then post a one-line summary of each to
> the dev channel on Slack."
>
> A 2.6B model on the phone chained GitHub and Slack through MCP and asked my approval
> before each call.

Tweet 2:
> The summaries come from the tool output, PR titles and metadata the GitHub call
> returned. The model never reaches for world knowledge, which is exactly why a small
> model does this without hallucinating. Orchestrate what the tools return. Nothing
> else.

Tweet 3:
> Setup was one Zapier MCP server with three actions, pasted into the app's Tools
> screen as a URL plus auth header. Fifteen minutes. Any streamable HTTP MCP server
> works the same way. [REPO LINK]

### LinkedIn post

> A useful test for any agent platform: can it do a real chore across two real
> systems without a human copying and pasting in the middle?
>
> Demo: "Check the open pull requests on our repo, then post a one-line summary of
> each to the dev channel on Slack." RunAnywhere Agent runs this as a chain: a GitHub
> call through MCP, summaries written from the returned titles and metadata, a Slack
> post through MCP. The model is 2.6B parameters and it runs on the phone. Each
> external call stops on an approval card until a human taps.
>
> Two design choices make this reliable on a small model. First, summaries are
> grounded in tool output only; the model is never asked to know anything. Second,
> the MCP server exposes three actions, not three hundred; routing accuracy scales
> inversely with tool-list size.
>
> Setup: one hosted MCP server (Zapier or Composio), URL and auth header pasted into
> the app's Tools screen. Fifteen minutes, once.
>
> Open source: [REPO LINK]

---

## Day 9, Finale: The Airplane Mode Gauntlet

**Hook:** One continuous session, airplane mode the whole way. Teach it a verb, arm a
watchdog, give it a fuzzy calendar problem, watch it wake itself mid-task, say the
verb, kill the app, and ask what it remembers. Every prior demo, one take.

**Feasibility: WORKS TODAY.** This is the live 7-minute show cut to 90 seconds.

### Storyboard

Setup checklist (the full show checklist):

- Model loaded, chat cleared
- Calendar seeded (Day 1 seed), calendar and notification permissions granted
- Do Not Disturb off, screen timeout 30 minutes
- Battery 30 to 80 percent
- Flashlight on before the take (the macro will kill it)
- App stays foregrounded throughout so the scheduled task can fire
- Rehearse the timing: arm the watchdog with +3 so it fires during the calendar beat

Exact utterances, in order:

1. > "Remember that I'm on 20mg of Lexapro, my therapist is Dr. Okafor, and my
   > appointment is Thursday at 4pm."
2. > "Check my battery now and remember it. Then in 3 minutes check it again and tell
   > me if it dropped more than 2 percent."
3. > "New rule: when I say wind down, set the brightness to 20 percent, turn the
   > flashlight off, and remind me to set my alarm."
4. > "Look at tomorrow. Find me 90 minutes for the gym that isn't before 10am and
   > isn't straight after standup, and put it in."
5. (watchdog fires by itself during 4)
6. > "Wind down."
7. (force-kill the app, reopen)
8. > "What do I need to remember about Thursday?"

Expected tool chain: the union of Days 1 through 4. The critical unscripted moment is
the scheduled-task card appearing on its own during the calendar turn.

Shot list:

| Shot | Length | On screen | Caption |
|---|---|---|---|
| 1 | 5s | Airplane mode on. Timestamp overlay starts and never leaves | "One session. Offline start to finish. The clock proves it." |
| 2 | 8s | Utterance 1, rail: memory saved, calendar written | "The demo Apple settled $250M over." |
| 3 | 8s | Utterance 2, rail: task scheduled | "It just made itself an appointment for 3 minutes from now." |
| 4 | 8s | Utterance 3, rail: macro defined | "New verb learned: wind down." |
| 5 | 12s | Utterance 4, rail reading calendar. Mid-turn, the scheduled-task card appears by itself, notification drops | "Nobody touched the phone. It woke itself mid-task." |
| 6 | 6s | Gym event in the real Calendar app | "And the 90 minutes landed where it should." |
| 7 | 7s | "Wind down." Screen dims, torch dies, reminder lands | "The taught verb, replayed as code." |
| 8 | 9s | App force-killed, reopened, recall question, answer names all three facts | "Killed the app. It still remembers. The memory is a file on this phone." |
| 9 | 7s | Model pill tapped, model manager with Hugging Face search | "And the brain is swappable. Open source. [REPO LINK]" |

Caption for the whole cut, first frame: "Condensed from an 8-minute session. Every
turn ran 15 to 45 seconds on a phone CPU."

### X thread

Tweet 1:
> One session. Airplane mode start to finish. A 2.6B model on a phone CPU:
>
> remembered my medication and my therapist, scheduled its own future task, learned a
> new verb, solved a two-constraint calendar problem, woke itself up mid-task,
> executed the verb, survived a force-kill, and recalled everything.

Tweet 2:
> None of these is a party trick alone. Together they are an operating loop: memory,
> deferred agency, taught behavior, judgment over your data. That loop is what people
> mean by "agent," and it just ran with the radio off.
>
> Condensed from 8 minutes. Every turn: 15 to 45 seconds, on a phone CPU.

Tweet 3:
> On-device AI was considered a novelty. "Hey, it can run on your phone." It now runs
> complete agentic systems. The whole thing is open source, and the model is
> swappable from a Hugging Face search inside the app. [REPO LINK]

### LinkedIn post

> This week we published eight demos of RunAnywhere Agent. Today's video is all of
> them in one continuous session, in airplane mode, with a timestamp on screen the
> entire time.
>
> In one take, a 2.6B-parameter model on a phone CPU: stored personal medical context
> and recalled it after a force-kill (the feature Apple advertised, never shipped, and
> settled roughly $250M over), scheduled itself a future task and woke up unattended
> to complete it, learned a new spoken verb and replayed it deterministically, and
> solved a calendar request with two fuzzy constraints, writing the result to the real
> calendar.
>
> Our position is simple. The industry decided agents live in datacenters before
> anyone seriously tried the alternative. A small model with good tools, precomputed
> structure where code beats generation, approval gates on side effects, and a
> retry harness does real agentic work on the hardware you already own. Turns take 15
> to 45 seconds and we show that instead of hiding it.
>
> Everything in these nine videos is in the open-source build today: [REPO LINK]
>
> The model is not even fixed. There is a Hugging Face search inside the app. Put a
> different brain in it.

---

## Publishing checklist (every day)

- [ ] Measured turn time from the actual take inserted wherever the copy says NN
- [ ] No emojis, no em dashes, none of the banned phrases
- [ ] Airplane-mode toggle uncut at the head of every offline video
- [ ] Latency caption present (real time or condensed, stated either way)
- [ ] No claim that it controls arbitrary apps, no world-knowledge answers on camera
- [ ] End card with [REPO LINK] rendered
- [ ] MCP days: dry run completed on the same server config that will be filmed
