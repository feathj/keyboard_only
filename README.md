Keyboard Only Development Training
==================================
Keyboard only access to software is one of the primary pillars of a11y.
It is not only important for visually impaired users who may not be able
to see where a mouse is interacting with the software, but it is
crucial for motor-impaired users who interact with software using a wide
variety of alternative input devices (puff and sip, eye trackers, or
switch devices)

* Tab
* Shift-Tab
* Arrow keys for drop-downs
* Enter to activate buttons or links

As with any a11y development, keep KB only navigation in the front of
your mind while you are implementing any UI you are working on.
Generally, if you are building simple forms, or other standard html
markup, most of the KB only navigation will be done for you, but here
are some of the basic gotchas to look out for:

1.  Tab order problems
2.  Focus traps
3.  Reverse track problems (tab order, focus traps, and other problems
_can_ only exist in the reverse path)

Tab, and tab order problems
===========================
Generally, tab order is handled automatically for you based on the
element's position in the DOM tree.  Even if you add elements
dynamically to the DOM, you will see that the browser will generally
handle the tab ordering for you. <demo1>

Where many tab order problems arise, is when the styling of an element
makes it appear in a different order than it's actual position in the
DOM. <demo2>  These types of issues are often resolved by fixing the
DOM order of the element to match the styling.

Explicit setting of the tabindex can also cause all kinds of bad.
Don't do it.  Even if you don't explicitly set the tab order in your
own code, watch for it in other markup merged into yours (sub-templates
etc).  Also watch for setting tab order to -1, which makes the field
un-tabable.

Sometimes explicitly setting the tab index to fix one focus problem
can cause another (see field 8)

Focus Traps
===========
Sometimes, a page will lose focus all-together.  This is a huge problem
to both visually impaired and motor impaired users that requires them
to go through the process of manually finding where they were prior to
focus being lost. It is most often caused by page logic switching focus
to another form (like a modal), and not explicitly setting the focus
back.  <demo> Note that many non-terrible modal or dialog libraries
will take care of this for you, but I have seen it break many times in
canvas.

Reverse Track Problems
======================
Much like other keyboard only problems, reverse track problems can be
caused by a wide variety of issues.  Using logic to explicitly set the
focus, and only accounting for the forward case seems to be the most
prevalent. <demo>

The obvious fix to this problem, is to not explicitly set the focus
when possible, but sometimes this is not a viable solution.
Introducing iframes, embedding javascript applications into existing
pages, introducing custom javascript components that set focus
explicitly, and other similar scenarios generally can't be avoided.

Re-cap
======
* Check for KO issues WHILE you implement your UI, not after
  * Be sure to check both forward and reverse tracks
  * Watch for focus traps (especially if a modal is involved)
* Don't lie to the DOM, and most of this won't be an issue
* Avoid explicit tabindex and focusing whenever possible