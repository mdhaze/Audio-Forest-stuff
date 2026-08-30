Audio Forest is a way to **listen** to the smoker instead of watching a screen.

You already have the hardware: smoker, Fireboard, two or three probes. This program does not replace the Fireboard app. It turns the same temperatures into a quiet background of sound so you can walk around, sit on the porch, or talk to someone and still know whether the pit and the meat are behaving.

It is not an alarm clock. Most of the time it should feel like weather — always there, easy to ignore. You only notice it when something changes.

## What you need

- The Fireboard and probes, as you already use them
- Those probe readings available in **Home Assistant** (that is how this page gets live numbers)
- A phone, iPad, or laptop with a speaker or headphones
- The file `index.html` opened in Safari (or another browser)

If Home Assistant is not set up yet, you can still run **Test Mode** and hear how the sounds work using a fake cook.

## What each sound means

**Low steady tone (the drone)**  
Pit / air temperature. It sits in the background the whole time the program is running. If the pit is falling and getting too low, the tone gets darker, and you will hear **three short breaks** in it. That means add wood.

**Soft hiss**  
The blower. Louder or brighter hiss means the controller is working harder. This is not the “add wood” signal.

**Birds**  
Each meat probe has its own bird.

- Meat 1 — short single chirp  
- Meat 2 — two-note rising tweet  
- Meat 3 — longer downward slide  

A bird only sings while that probe is live. Calls are irregular, somewhere in a one-minute window. If the meat is climbing, the call lifts. If it is falling, the call droops. When that piece of meat is **done** (hits the target you set), that bird switches to fast, urgent calling.

If you pull a probe out of the meat or unplug it from the Fireboard, **that same bird complains** — a short burst of falling calls. That is how you learn which voice is which without looking.

**Soft bongos**  
About once a minute, a little group of four or five hits. That only means the program is still running. If the bongos stop and everything else goes dead, the page is no longer live.

## How to run a real cook

1. Open the current `index.html`. The comment at the top of the file is the version (currently **v1.31**).
2. Open Settings (gear).
3. Turn **Test Mode off**.
4. Enter your Home Assistant URL and long-lived token.
5. Set meat targets (for ribs, 195 is a typical finish). `0` means that probe is ignored for “done.”
6. Close Settings. Press **Start**.

The status line must say **Live**. If it says **Test**, you are hearing the fake cook, not the Fireboard.

Right now the live sensors are wired as:

- Air — `sensor.14_texas_smoker_v_m_shelf_center`
- Meat 1 — `sensor.14_texas_smoker_meat_1_ch1`
- Meat 2 — `sensor.14_texas_smoker_meat_2_ch2`
- Meat 3 — `sensor.14_texas_smoker_vertical_lower_tray`

If a probe does not show up on the page, Home Assistant is not publishing that entity, or the name does not match.

## How to practice without a fire

Turn **Test Mode on**. Press Start. The built-in sample cook will play. **Accelerated** runs it fast so you can hear “add wood,” a stage change, and “done” without waiting hours. This is for learning the sounds. Turn Test Mode off before a real pack of ribs.

## What not to expect

It will not talk. It will not say “205 degrees.” It will not replace glancing at the Fireboard when you want an exact number.

It will tell you, by ear:

- the fire is alive  
- the fire is fading (add wood)  
- this rack is still cooking  
- this rack is done  
- this probe just came out or went dead  
- the program itself is still running  

That is the whole point: two or three pieces of meat, one pit, and a soundscape thin enough that you can live with it for a six-hour cook.
