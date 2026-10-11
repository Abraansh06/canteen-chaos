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



### CC-02 — "<dark mode dish text problem>"

**Reproduced:** When switching from light mode to dark mode; the dish text doesn't change according to the given mode, which makes it difficult to read. 

**Cause:** In `frontend/style.css` , `.dish-body` had a `hardcoded color` around black, instead of using themed variable.
 
**Fix:** I Replaced the hardcoded hex code with `color: var(--ink);` on `.dish-body` so it automatically shifts to light color text when dark mode is toggled.

**Checked:** Toggled dark mode in the browser. Dish titles, descriptions, and pricing now appear in the proper light font color with clear contrast.

**Time:** It took around 10 minutes, as most of the portion was just to find the `dish-body` class selector.


### CC-01 — "<Search suggestions behind everthings>"

**Reproduced:** When searching for any specific item, when suggestions start to appear but user can't see them due to positioning problem.

**Cause:** In `frontend/style.css` , `#catTabs` z-index was 40 whereas in `.search-wrap` z-index was 1 due to which it appeared to be hidden behind the category tabs.
 
**Fix:** I modified the `z-index` of `search-wrap` from 1 to 50 , although we can take any number greater than 40. 

**Checked:** When searching for any item, the suggestions comes after tabs.

**Time:** It took around 5 minutes.

### CC-09 — "pagination slicing broken"

**Reproduced:** Loading next page or scrolling loaded the full dish list repeatedly instead of discrete item chunks.

**Cause:** In `backend/logic/search.js`, `paginate()` correctly sliced the array into `const items = list.slice(...)` but erroneously returned `items: list`.

**Fix:** Changed line 93 in `backend/logic/search.js` from `items: list` to `items: items`.

**Checked:** Verified via browser and API responses that each page payload now strictly respects pagination bounds (`limit: 12`).

**Time:** Around 10 minutes.


### CC-10 — "Inverted price sorting"

**Reproduced:** Selecting "Price: Low to High" ordered items in descending order, and vice-versa.

**Cause:** In `backend/logic/search.js`, the comparator functions inside `SORTERS` for `price-asc` and `price-desc` had reversed subtraction operands.

**Fix:** Swapped `SORTERS['price-asc']` to `(a, b) => a.price - b.price` and `SORTERS['price-desc']` to `(a, b) => b.price - a.price`.

**Checked:** Verified in browser dropdown that menu items now sort properly in both ascending and descending order.

**Time:** Around 15 minutes.


### CC-04 — "Buttons unresponsive on tablet viewports"

**Reproduced:** On viewport widths between 761px and 900px, clicking or tapping "Add to Cart" and the favorite star button on dish cards did nothing.

**Cause:** In `frontend/style.css`, the media query `(min-width: 761px) and (max-width: 900px)` created `.dish-card::after` and `.img-wrap::after` pseudo-elements with positive z-index values directly over the buttons without `pointer-events: none`, intercepting all click and touch events.

**Fix:** Added `pointer-events: none;` to `.dish-card::after` and `.img-wrap::after` inside the tablet media query in `frontend/style.css`.

**Checked:** Tested in browser responsive mode at 800px width. Verified that clicking the favorite star button toggles favorites and "Add to Cart" correctly adds items to the cart.

**Time:** 10 minutes



## CC-05 — "Category and filter bar scrolls away on mobile"

**Reproduced:** On mobile screen sizes, the category and filter bar scrolled off-screen instead of sticking beneath the header.

**Cause:**
1. `.filters` was set to `top: 0` (sliding under `.site-header`) instead of accounting for the full header height (`93px` including `.slot-bar`).
2. Inside `@media (max-width: 480px)`, `.view` had `overflow-x: hidden;`, which prevented elements with `position: sticky` from functioning properly.

**Fix:** 
1. Updated `.filters` in `frontend/style.css` to `top: 93px;`.
2. Removed `overflow-x: hidden;` from `.view` under `@media (max-width: 480px)`.

**Checked:** Tested scrolling across mobile viewport widths (375px–480px); the category and filter bar remains pinned cleanly under the header without overlap.

**Time:** 25 minutes


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
