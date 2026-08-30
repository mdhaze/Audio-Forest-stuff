[README.md](https://github.com/user-attachments/files/31618316/README.md)
# Audio Forest — Beginner Guide 1.35

For someone who already has a smoker, a Fireboard, and a couple of meat probes.

Working program: `index.html` (**v1.35**). Design manifesto: `Audio_Forest_Starter_Document.md`. Practice cook: `Three_Rack_Ribs_Drill.xlsx`.

---

Audio Forest is a way to **listen** to the smoker instead of watching a screen.

It does not replace the Fireboard app. It turns the same temperatures into a quiet background of sound so you can walk around, sit on the porch, or talk to someone and still know whether the pit and the meat are behaving.

It is not an alarm clock. Most of the time it should feel like weather — always there, easy to ignore. You only notice it when something changes.

## What you need

- The Fireboard and probes, as you already use them
- Those readings available in **Home Assistant** (that is how live numbers get into this page)
- A phone, iPad, or laptop with a speaker or headphones
- The file `index.html` opened in Safari or another browser

If Home Assistant is not set up yet, use **Test Mode** and a practice spreadsheet.

## What you see

Two large numbers at the top, readable across a room:

- **Current time** (hours and minutes, no seconds)
- **Minutes running** since you pressed Start (shows — when stopped)

Each live meat probe then shows:

- Temperature and target, or DONE
- A second quiet line: cook-time as **°F·minutes above 140°F** (F-min)

Cook-time only counts while the probe is above 140°F. A probe sitting in room air, or pulled from the meat, adds nothing. **Reset cook-time** zeroes those counters. Hit it at the start of a pack.

## F-min is data only

F-min is **not** a definition of done. Done is still target temperature, stage time, or how the meat feels.

The number is:

`Σ max(0, probe °F − 140) × minutes`

It is a progress meter and a way to compare racks on the same cook. It is a bad substitute for 195°F.

Do not treat `(195 − 140) × 120 = 6,600` as a finish line. That assumes two hours sitting at a flat 195°F and that every degree above 140 counts equally. Collagen conversion is not linear. Three different temperature paths can print the same 6,600 and not be the same meat. A normal pack of ribs that you pull when it first hits 195 will usually show a **much smaller** F-min than 6,600, because most of the cook is spent closer to 160–175 than to 195.

**Log F-min at the moment you actually pull.** Write down the rack, the finish temp, and the F-min on the screen. After a few of your own cooks that log is what makes the number mean something. Until then it is just a notebook.

## What each sound means

**Quiet drone**  
Pit / ambient air, presence only. Kept low so it does not dominate.

**Morse on the pit**  
When air is more than about **10°F off setpoint**:

- Too low — Morse **S** (···) about every 30 seconds. Add wood.
- Too high — Morse **O** (———) about every 30 seconds.
- **25°F or more off** — same letter, louder and more often (about every 12 seconds).

Inside the ±10°F band there is no Morse. The old three-break “add wood” drone stutter is gone.

**Soft hiss**  
The blower. Brighter or louder hiss means the controller is working harder. This is not the add-wood signal.

**Birds**  
Each meat probe has its own bird.

- Meat 1 — short single chirp
- Meat 2 — two-note rising tweet
- Meat 3 — longer downward slide

A bird only sings while that probe is live. Spacing is random, 15–60 seconds. Rising meat lifts the call. Falling meat droops it. When the last stage ends (time limit or target, whichever comes first), that bird switches to fast urgent calling.

If you pull a probe out of the meat or unplug it from the Fireboard, **that same bird complains** — five falling calls, close together. That is how you learn which voice is which. At most once per 20 seconds per probe.

**Soft bongos**  
One group of four or five hits, about once a minute. Means only that the program is still running. If they stop and the rest of the stream dies, the page is no longer live.

## Probe numbering

In the spreadsheet and in your own notes:

| Probe # | Column | Meaning |
|--------|--------|---------|
| 0 | `Probe0_F` | Ambient / pit air |
| 1 | `Probe1_F` | Meat 1 |
| 2 | `Probe2_F` | Meat 2 |
| 3 | `Probe3_F` | Meat 3 |

Old files that still say `AirTemp_F` will import.

## How to run a real cook

1. Open `index.html`. The comment at the top of the file must say **v1.35**.
2. Settings (gear). Turn **Test Mode off**.
3. Home Assistant URL and long-lived token.
4. Meat targets (195 is typical for ribs). `0` means that probe is not used for DONE.
5. Close Settings. Press **Start**.
6. When you pull a rack, write down its F-min. Do not reset cook-time until the pack is finished or you will lose the log.

The status line must say **Live**. If it says **Test**, you are hearing a fake cook.

Current Home Assistant entities:

- Probe 0 (air) — `sensor.14_texas_smoker_v_m_shelf_center`
- Probe 1 — `sensor.14_texas_smoker_meat_1_ch1`
- Probe 2 — `sensor.14_texas_smoker_meat_2_ch2`
- Probe 3 — `sensor.14_texas_smoker_vertical_lower_tray`

If a probe does not appear, the entity name does not match or Home Assistant is not publishing it.

## How to practice without a fire

1. Settings → Import `.xlsx` → `Three_Rack_Ribs_Drill.xlsx`
2. Confirm the label shows **Three-rack ribs drill**, not Built-in SAMPLE
3. **Test Mode on**. **Accelerated on**.
4. Start.

That series walks the pit up, sags it (Morse S), runs three birds, pulls Meat 3 (complaint), then takes Meat 1 and Meat 2 to DONE.

First import needs a network connection so the spreadsheet library can load. After that the series is saved in the browser.

Turn Test Mode off before a real pack of ribs.

## What not to expect

It will not talk. It will not say “205 degrees.” It will not replace the Fireboard when you want an exact number.

It will tell you, by ear:

- the fire is alive
- the fire is too low (Morse S) or too high (Morse O)
- this rack is still cooking
- this rack is done
- this probe just came out or went dead
- the program itself is still running

And by glance:

- what time it is
- how many minutes this run has been going
- how much time each rack has spent above 140°F

That is the whole point: two or three pieces of meat, one pit, and a soundscape thin enough to live with for a six-hour cook.
