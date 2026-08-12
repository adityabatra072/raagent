# RunAnywhere Agent — Demo Pack

The show is 7 minutes. Every beat is chosen to be **impossible for Siri or Gemini**,
not merely *nice*. Read the "Rules" section before adding anything.

---

## The thesis (say this first, in one breath)

> This is a base iPhone 15 — a phone Apple says is too weak for Apple Intelligence.
> There's a 2.6-billion-parameter model running inside this app. In a second there'll
> be no internet either. Everything you're about to see is that model deciding what
> to do and doing it.

Three facts that make the room lean in, all verifiable:

| Fact | Why it lands |
|---|---|
| Apple Intelligence requires iPhone 15 **Pro** or 16+. A base 15 gets none of it. | The demo device is one Apple wrote off. |
| The LLM Siri rewrite is Gemini-on-Private-Cloud-Compute — i.e. **cloud** — and still hasn't shipped to consumers (delayed past iOS 26.4; Apple settled a ~$250M false-advertising suit over the personal-context demo it showed and never delivered). | Their answer to this problem is a server. Ours is the phone. |
| Google retires Assistant for Gemini in Sept 2026; Samsung's "first agentic AI phone" routes to the cloud too. | Every shipping competitor needs a network. |

---

## Rules (learned from an adversarial review — violate these and you lose the room)

1. **Never demo something Siri does well.** Timers, alarms, "open Spotify", plain
   reminders, unit conversion. If it fails you look broken; if it works you look redundant.
2. **Never demo world knowledge.** A 2.6B model will hallucinate; the audience will
   compare it to ChatGPT and you lose.
3. **Never claim "it can control any app."** That's the Rabbit R1 obituary.
4. **Let the audience drive.** A judge flips airplane mode and types their own sentence.
   Staging accusations die instantly.
5. **Latency is theater, not shame.** A turn takes ~15–45s on device. Narrate the
   action rail while it runs: "watch — it just decided to check the battery." Never
   stand in silence, and never say "sorry, it's slow."
6. **The tool counts, the model judges.** Clock arithmetic, gap-finding and track
   resolution are done in code on purpose. Say so — it's engineering maturity, and it's
   why the demo doesn't collapse on a small model.

---

## Setup checklist (do this before anyone is watching)

- [ ] Model downloaded and **loaded** (open the app once; first load takes ~30s)
- [ ] Calendar permission granted, with 3–4 events on tomorrow's calendar
  (e.g. Standup 09:30–10:00, Design review 11:00–12:00, 1:1 15:00–15:30)
- [ ] Notification permission granted
- [ ] Spotify installed and logged in (only for the optional connected beat)
- [ ] Screen timeout set to 30 min; Do Not Disturb **off** (the watchdog banner must land)
- [ ] Battery between 30–80% so the watchdog has room to move
- [ ] Chat cleared

---

## Running order

| Time | Beat | Network |
|---|---|---|
| 0:00 | Cold open — judge flips airplane mode | ✈️ off |
| 0:30 | **1. The lawsuit demo** — private dictation, stored locally | ✈️ off |
| 1:45 | **2. The watchdog** — arm it, then walk away | ✈️ off |
| 2:30 | **3. Teach it a verb** — "wind down" | ✈️ off |
| 3:30 | **4. Calendar judgment** — fuzzy constraints (watchdog fires here) | ✈️ off |
| 5:00 | **3b. Say "wind down"** — the taught verb executes | ✈️ off |
| 5:45 | **1b. Force-kill the app, then recall** | ✈️ off |
| 6:30 | Closer — hand the phone over | ✈️ off |

Optional pre-roll if the room needs a warm-up (**network on**, before the cold open):
the Spotify chain — see "Bench" at the bottom.

---

## 1. The demo Apple settled a lawsuit over

**Utterance (a judge says it, in their own words — this is the point):**
> "Remember that I'm on 20mg of Lexapro, my therapist is Dr. Okafor, and my appointment
> is Thursday at 4pm."

**Under the hood:** `remember(fact)` → `calendar_create(title, start)`

**On screen:** two amber lines on the action rail — *Saving to memory → Saved on this
phone*, then *Adding "Dr. Okafor" to calendar → Event added* — then one sentence of
confirmation.

**Say while it runs:** "That sentence went to a model running on this phone. There is no
request to inspect, because there's no network and no server."

**Part 2 (at 5:45, after force-quitting the app):**
> "What do I need to remember about Thursday?"

`recall(query)` → answer naming Dr. Okafor, 4pm, and the dosage.

**Why it beats Siri:** this is verbatim the personal-context feature Apple demoed in
2024, pulled from its own ad, delayed indefinitely, and paid to settle. Here it runs
offline on the phone Apple excluded — and the fact survives the app being killed.

**Failure mode:** if `recall` returns the wrong fact, the store is a flat list — say
"it keeps everything; let me show you" and ask *"what have I told you to remember?"*
It will list them. Recovery reads as transparency.

---

## 2. The watchdog (deferred agency — the strongest technical beat)

**Utterance:**
> "Check my battery now and remember it. Then in 3 minutes check it again and tell me
> if it dropped more than 2 percent."

**Under the hood:** `device_info` → `remember("battery was N%")` → `schedule_task(instruction, when="+3")`

Three minutes later the app **wakes itself**, runs a *fresh agent loop* with the whole
tool set: `device_info` → `recall` → compares → `send_notification`.

**On screen at fire time:** a bordered "scheduled task · running now" card appears in the
chat *by itself*, the rail ticks through its steps, and a system notification drops.

**Say when it fires (mid-demo 4 — do not flinch, point at it):** "That's the model waking
itself up. Nobody touched the phone. It just re-read a number it wrote down three minutes
ago and made a call on it."

**Why it beats Siri:** Siri cannot schedule *reasoning*. A Shortcuts automation can
trigger on a battery threshold, but it cannot compare against a baseline it recorded
because you said a sentence, and it cannot decide what "dropped more than 2 percent"
means at fire time.

**Timing:** arm it at 1:45 with `+3` so it lands around 4:45, inside demo 4. Rehearse
the offset — if your machine runs slower, use `+4`.

**Failure mode:** the app must stay in the foreground for the wake (documented limit —
iOS suspends background apps). Keep the agent screen up. If it doesn't fire, say
"it fires when the app is alive — that's an OS constraint, not a model one" and trigger
it by re-opening the app (overdue tasks run on launch).

---

## 3. Teach it a verb it doesn't have

**Utterance (teaching):**
> "New rule: when I say wind down, set the brightness to 20 percent, turn the flashlight
> off, and remind me to set my alarm."

**Under the hood:** `define_macro(name="wind down", steps=[set_brightness, flashlight, send_notification])`

**Utterance (executing, ~2 minutes later):**
> "Wind down."

**Under the hood:** `run_macro("wind down")` → all three fire in one step.

**On screen:** the screen visibly dims, the torch dies, a reminder notification lands —
within a couple of seconds of each other.

**Say:** "I just programmed my phone by talking to it. No Shortcuts editor, no automation
builder, no account. And that macro is a file on this device."

**Why it beats Siri:** Siri cannot be taught a new verb. Shortcuts can — by opening an
editor and dragging blocks.

**Engineering note (worth saying out loud if the audience is technical):** the model
records the steps *once*; replay is deterministic. A 2.6B model re-planning four actions
on every invocation would be slow and drift. Teach once, replay forever.

**Failure mode:** if the model defines the macro with a wrong tool name, the tool returns
the available list and it retries — visible on the rail as a second attempt. That's the
harness self-correcting; narrate it as such.

---

## 4. Calendar judgment under fuzzy constraints

**Utterance:**
> "Look at tomorrow — find me 90 minutes for the gym that isn't before 10am and isn't
> straight after standup, and put it in."

**Under the hood:** `calendar_query("tomorrow")` — the *tool* returns events plus
precomputed free gaps ("11:20–13:00, 100 min") — model picks the gap satisfying both
constraints → `calendar_create`.

**On screen:** the rail shows the calendar being read, then the event being written.
Open the Calendar app afterwards to show the block sitting there.

**Say:** "It didn't just find a hole in the day. It found one that satisfies two
constraints I expressed as opinions, not filters."

**Why it beats Siri:** "find a time" exists everywhere; "not before 10, not straight
after standup" is judgment. Siri cannot read your calendar, reason about it, and write
back in one instruction.

**Cut this one first if you're running long** — it's the most build-dependent and the
most sensitive to a bad calendar state.

---

## Closer

Hand the unlocked phone to whoever flipped airplane mode.

> "Delete the app and everything I told it tonight is gone. There's no server to ask,
> no account to close, no request log. It ran on a phone Apple said couldn't do this."

Then, in one sentence, tap the model pill → Models: "and it isn't hardcoded to one
model — that's a Hugging Face search, on the phone; you can put a different brain in it."
**Do not** start a download on venue wifi.

---

## Bench (kept working, deliberately not headlined)

These must never fail, but none of them is a *reason* to be impressed — Siri does them.
Use them only to answer "but can it do normal stuff?"

- **Spotify:** "Play Janice STFU on Spotify" → the tool resolves the real
  `spotify:track:` URI and playback starts. (Requires network.)
- Flashlight, brightness, battery/storage status, timers, alarms, notifications.
- Email/SMS/call: composes and **pauses for approval** — the confirmation card is the
  interesting part, so if you show it, show the card and the fact that the run stops.
- Web search → answer chain (requires network).

---

## What we deliberately do NOT demo

| Rejected | Reason |
|---|---|
| "Find Drake's latest song and play it" as a hero beat | Siri does it in 2 seconds, needs the network anyway, and it's where a 2.6B most likely hallucinates a title. Kept on the bench, not in the show. |
| Model writes and runs code (compound interest) | It's a calculator to the audience, and "LLM runs generated code on my phone" is a liability, not a flex. Cut entirely. |
| Trivia / current events | Cloud wins; small models hallucinate. |
| Image generation, translation, dictation | OS built-ins. |
| Model download as the closer | Never close on a progress bar over venue wifi. |
| "It can control any app" | Rabbit R1 territory. We name our tools honestly. |

---

## Honest limits (have these ready — being straight about them buys credibility)

- **Latency:** ~15–45s per agent turn on device. Multi-step demos take minutes. This is
  a 2.6B model on a phone CPU; the NPU path (QHexRT on Snapdragon) is the roadmap answer.
- **Scheduled tasks need the app alive.** iOS suspends background apps; overdue tasks run
  on next launch.
- **Web tools need the network** — in airplane mode the agent says so plainly instead of
  inventing an answer.
- **It is not a frontier model.** Ask it to write your thesis and it will disappoint. It
  is a *doer*, not an oracle — that framing is the demo.
