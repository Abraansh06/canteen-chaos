# Debug log

Your notes. One entry per bug you fixed, using the template below.

This file is read as carefully as your code. A correct fix you cannot
explain counts for little; a bug you could not fix but investigated
honestly still counts for something.

Delete the example before you submit.



## Example — delete this

### CC-99 — "The cart total is wrong"

**Reproduced:** Added 2 dosas at Rs. 60 each. The cart showed
Rs. 119.99999 instead of Rs. 130. Happened every time, on any dish with
a price ending in .50.

**Cause:** The total was being added up with plain floating point and
never rounded, so 0.1 + 0.2 style errors showed up on screen. The
rounding helper existed but this one place was not using it.

**Fix:** Ran the total through the existing rounding helper instead of
adding a new one, so every price on screen goes through the same path.

**Checked:** Cart, checkout and the order screen all show Rs. 130 now.
Prices without decimals still show without a trailing .00.

**Time:** about 40 minutes, most of it working out that the cart and the
order screen round in different places.



## CC-02 — "<dark mode dish text problem>"

**Reproduced:** When switching from light mode to dark mode; the dish text doesn't change according to the given mode, which makes it difficult to read. 

**Cause:** In `frontend/style.css` , `.dish-body` had a `hardcoded color` around black, instead of using themed variable.
 
**Fix:** I Replaced the hardcoded hex code with `color: var(--ink);` on `.dish-body` so it automatically shifts to light color text when dark mode is toggled.

**Checked:** Toggled dark mode in the browser. Dish titles, descriptions, and pricing now appear in the proper light font color with clear contrast.

**Time:** It took around 10 minutes, as most of the portion was just to find the `dish-body` class selector.



## Could not fix

For anything you investigated but did not solve. Say what you tried and
where you got to. This is worth marks — leaving it blank when you got
stuck is not.

### CC-0X — "<the complaint>"

**What I tried:**

**Where I got to:**

**What I would try next:**



## Extra credit

Anything not on the bug log: a problem you found yourself, a test you
wrote, or a fix you are unsure about. Same format, plus one line on how
you noticed it.
