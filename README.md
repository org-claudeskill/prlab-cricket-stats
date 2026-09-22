# cricket-stats (hop 2)

Match ledger. **Two hops** from `cricket-protocol`. **One hop** from `cricket-scoring`.

Copies `ScoreSnapshot.runs` / `wickets` / `overs` for hop 3 (`cricket-fantasy`). Does not import the protocol package. Does not re-interpret appeals.

If scoring counted a wicket that was not given, this ledger will copy that total and fantasy will pay for it. This repo cannot see that.

## Contract with hop 3

`GET /matches/{id}/ledger` returns `{ match_id, runs, wickets, overs }` only. Do not add `last_event`, `raw_ball`, or `umpire_confirmed`. Fantasy will start depending on them.

## Trap branch

`trap/count-not-out-as-wicket` — treat `last_event.display == "NOT_OUT"` as a dismissal "because DRS usually upholds". Stats tests stay green. Fantasy then awards bowling points for an appeal that scoring said was not out.

## Develop

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"
pytest
uvicorn stats.app:app --port 8001
```
