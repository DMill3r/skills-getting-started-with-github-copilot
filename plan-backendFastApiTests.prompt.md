## Plan: Add FastAPI backend tests

TL;DR - Create a new top-level `tests/` directory and add Pytest-based FastAPI endpoint coverage for `src/app.py` using `fastapi.testclient`.

**Steps**
1. Create `tests/test_app.py`.
   - Import `TestClient` from `fastapi.testclient`.
   - Import `app` from `src.app`.
   - Instantiate `client = TestClient(app)`.
2. Add backend endpoint tests.
   - `test_get_activities_returns_200_and_activity_data`: verify GET `/activities` returns status 200 and includes known activity keys.
   - `test_signup_for_activity_adds_participant`: sign up a new email, verify status 200, response message, and that GET `/activities` includes the new participant.
   - `test_signup_duplicate_returns_400`: sign up an already-registered email and confirm status 400 with error detail.
   - `test_signup_unknown_activity_returns_404`: POST to unknown activity and confirm status 404.
   - `test_remove_participant`: delete an existing participant, verify status 200 and that participant is removed from GET data.
   - `test_remove_unknown_participant_returns_404`: DELETE a non-existent participant and confirm status 404.
3. Ensure tests use a fresh or isolated copy of the in-memory `activities` state if needed.
   - If necessary, import the module and reset or reuse `src.app.activities` between tests.
4. Verify tests run with `pytest tests` from repository root.

**Relevant files**
- `/workspaces/skills-getting-started-with-github-copilot/src/app.py` — API implementation under test
- `/workspaces/skills-getting-started-with-github-copilot/pytest.ini` — existing pytest config
- `/workspaces/skills-getting-started-with-github-copilot/tests/test_app.py` — new test file

**Verification**
1. Run `pytest tests` and confirm all tests pass.
2. Confirm the new `tests/test_app.py` file is discovered by Pytest.
3. Optionally, confirm endpoint behavior manually by starting the app and exercising the same API calls.

**Decisions**
- Use `fastapi.testclient.TestClient` for backend API tests.
- Keep tests in a new separate `tests/` directory as requested.
- Reuse the current in-memory activity data by resetting shared state if needed.
