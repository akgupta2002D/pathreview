## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/117

**Issue title:** API docs don't include example `curl` commands

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The API reference in `docs/API.md` documents each endpoint’s purpose and
parameters, but it never shows how to call them. Without sample `curl`
invocations, someone bringing the project up for the first time has no quick
way to confirm the server is responding as expected. Filling in those
examples would make the docs a practical smoke-test guide as well as a
reference.

**Is this right for me?**
- [x] Scope is clear — one file (`docs/API.md`); add example `curl` calls for documented endpoints
- [x] Effort fits — labeled Tier 1 / good first issue; estimated 2–3 hours
- [x] Skills match — documentation + basic HTTP/`curl`; no deep backend or RAG changes required
- [x] Verifiable — I can run the API locally and confirm each example returns a sensible response
- [x] Unblocked — app setup is confirmed; work does not depend on unfinished features elsewhere

**Selection notes:** This is a focused docs gap rather than a bug hunt. The API surface in
`docs/API.md` is small (health, auth, profiles, reviews), so adding copy-pasteable
examples is a concrete, reviewable change that still teaches me the real request shapes
and auth flow. That makes it a good first contribution without overcommitting scope.

**Branch name:** docs/add-journal

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduce & plan

**Reproduction steps:**
1. Opened `docs/API.md` and confirmed every endpoint is described with no example `curl` invocations.
2. With the API running locally, ran:
   ```bash
   curl -s http://localhost:8000/health
   ```
3. Received a JSON health payload (HTTP 503 / `"status":"unhealthy"`) with
   `postgres` and `redis` marked unhealthy and `vector_db` healthy. That
   proves the API is reachable; the unhealthy flags look like known probe bugs
   (#154 SQLAlchemy `text()` usage, #155 missing `redis_host` on Settings), not
   a missing-docs problem.
4. Gap location: `docs/API.md` only — listings for Health, Auth, Profiles, and
   Reviews with no copy-pasteable examples.

**What a successful fix will add:** Working `curl` examples under each endpoint
section so a first-time setup can smoke-test the API from the docs alone.
