# Resilient Software

All software breaks. Developers may have introduced bugs in the code. Users may have used the software in ways that was never imagined. It is often not even the fault of any one person: the network connection may be lost partway through some transaction, leaving the system in a partially completed state.

Software that is **resilient** is able to remain tolerably functional in the face of failures. Just as our bodies have an immune system to counter illness, we can build immunity into the software through mechanisms such as recovery (taking corrective action after an error) and redundancy (trying again or deferring to a fallback system).

We will learn how to build software that can fend for itself when it is released into the wild by anticipating common errors and gracefully handling unexpected errors. We will employ practices that mitigate the impact that errors have on the overall health of our systems.
