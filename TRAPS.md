# Traps for single-repo review

## `trap/count-not-out-as-wicket`

**The PR:** analytics wants appeal volume. If `last_event.display` is `NOT_OUT`, increment `wickets` anyway — "most referrals are upheld". Unit test added.

**What a hop-2 review usually says:** product analytics, uses a field scoring already sends, tests updated, LGTM.

**1 hop up (scoring):** `wicket_counted` is ignored. Scoring published NOT_OUT on purpose.

**1 hop down (fantasy, hop 3 from protocol):** bowling points use `ledger.wickets`. An appeal becomes 20 fantasy points.

**3 hops up (protocol):** a later default on `umpire_confirmed` can make scoring say WICKET *and* this trap can make leftover NOT_OUT rows count too. Review of *this* PR cannot see fantasy.

**Functional truth:** hop 2 copies scoring totals. It does not decide who is out.
